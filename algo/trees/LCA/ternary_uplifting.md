**TERNARY UPLIFTING:**
--

Just like binary uplifting \
But now we do up[i][j] : as go to 3^j ancestor from the ith node
up[i][j] = up[up[up[i][j - 1]][j - 1]][j - 1]

