2D SEGMENT TREE
--

-> Example visulization:

![image](https://user-images.githubusercontent.com/94597499/147928853-0116415d-6ac0-490f-9204-ef340c3a6652.png)
![image](https://user-images.githubusercontent.com/94597499/147928979-1695b5ec-b691-4b94-b10f-03c755822c77.png)

-> make ordinary seg tree with respect to the first indices, and for each segment we build an ordinary seg tree w.r.t the second indices.\
-> for ex, if a 2d matrix a[0...n-1,0...m-1] is given, and we have to find sum/min/max on some submatrix a[x1...x2,y1...y2] as well as perform modifications of individual matrix elements (a[x][y]=p)\
-> after constructing an ordinary 1d seg tree using only the 1st coordinate let's say the first coordinate is alreasy fixed to some interval [l...r], then we actually build a seg tree for such a strip a[l...r,0...m-1]

1. BUILD:
---
```cpp
void build_y(int vx, int lx, int rx, int vy, int ly, int ry) {
    if (ly == ry) {
        if (lx == rx)
            t[vx][vy] = a[lx][ly];
        else
            t[vx][vy] = t[vx*2][vy] + t[vx*2+1][vy];   //since we need to cover all first coordinate's that contribute to this range of 2nd coordinate
    } else {
        int my = (ly + ry) / 2;
        build_y(vx, lx, rx, vy*2, ly, my);
        build_y(vx, lx, rx, vy*2+1, my+1, ry);
        t[vx][vy] = t[vx][vy*2] + t[vx][vy*2+1];
    }
}

void build_x(int vx, int lx, int rx) {
    if (lx != rx) {
        int mx = (lx + rx) / 2;
        build_x(vx*2, lx, mx);
        build_x(vx*2+1, mx+1, rx);
    }
    build_y(vx, lx, rx, 1, 0, m-1);
}
```
**COMPLEXITY:** 16nm

2. PROCESSING QUERY:
---
-> break query on first coordinate first, then for every reached vertex call the corresponding seg tree of the 2nd coordinate.
```cpp
int sum_y(int vx, int vy, int tly, int try_, int ly, int ry) {
    if (ly > ry) 
        return 0;
    if (ly == tly && try_ == ry)
        return t[vx][vy];
    int tmy = (tly + try_) / 2;
    return sum_y(vx, vy*2, tly, tmy, ly, min(ry, tmy))
         + sum_y(vx, vy*2+1, tmy+1, try_, max(ly, tmy+1), ry);
}

int sum_x(int vx, int tlx, int trx, int lx, int rx, int ly, int ry) {
    if (lx > rx)
        return 0;
    if (lx == tlx && trx == rx)
        return sum_y(vx, 1, 0, m-1, ly, ry);
    int tmx = (tlx + trx) / 2;
    return sum_x(vx*2, tlx, tmx, lx, min(rx, tmx), ly, ry)
         + sum_x(vx*2+1, tmx+1, trx, max(lx, tmx+1), rx, ly, ry);
}
```
**COMPLEXITY:** O(lognlogm)

3. MODIFICATION QUERY:
---
-> a[x][y] = p\
-> changes occur only in those vertices of the first seg tree that cover the coordinate x(O(logn)) and for seg trees corresponding to them the changes will only occur at those vertices that cover coordinate y(O(log m))\
-> descend the first coordinate and then the second

```cpp
void update_y(int vx, int lx, int rx, int vy, int ly, int ry, int x, int y, int new_val) {
    if (ly == ry) {
        if (lx == rx)
            t[vx][vy] = new_val;
        else
            t[vx][vy] = t[vx*2][vy] + t[vx*2+1][vy];
    } else {
        int my = (ly + ry) / 2;
        if (y <= my)
            update_y(vx, lx, rx, vy*2, ly, my, x, y, new_val);
        else
            update_y(vx, lx, rx, vy*2+1, my+1, ry, x, y, new_val);
        t[vx][vy] = t[vx][vy*2] + t[vx][vy*2+1];
    }
}

void update_x(int vx, int lx, int rx, int x, int y, int new_val) {
    if (lx != rx) {
        int mx = (lx + rx) / 2;
        if (x <= mx)
            update_x(vx*2, lx, mx, x, y, new_val);
        else
            update_x(vx*2+1, mx+1, rx, x, y, new_val);
    }
    update_y(vx, lx, rx, 1, 0, m-1, x, y, new_val);
}
```
**COMPLEXITY:** O(log n log m)


