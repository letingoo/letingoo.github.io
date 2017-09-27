---
layout: post
title: leetcode 542 —— 01 Matrix
---


1. 首先遍历矩阵，进行一次变换：遇到0不变，遇到1则将元素设成一个很大的值即可。同时，将0元素的row和col值放入队列中。
2. 遍历队列，取出队列中的一个坐标，查看其对周围上下左右的影响，看看能不能让周围的值更新为自己的值+1（只有周围的值比自己大才会更新）。直至队列为空。


代码如下：

```
    public int[][] updateMatrix(int[][] matrix) {

        if (matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0)
            return null;

        Queue<int[]> queue = new LinkedList<int[]>();

        int rows = matrix.length;
        int cols = matrix[0].length;


        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j] == 0) {
                    queue.offer(new int[]{i, j});
                }
                else if (matrix[i][j] == 1) {
                    matrix[i][j] = Integer.MAX_VALUE;
                }
            }
        }


        int[][] directions = new int[][]{{-1,0}, {1,0}, {0,-1}, {0,1}};
        while ( !queue.isEmpty() ) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int[] cur = queue.poll();
                for (int[] dir : directions) {
                    int x = cur[0] + dir[0];
                    int y = cur[1] + dir[1];

                    if (x < 0 || x >= rows || y < 0 || y >= cols)
                        continue;

                    int value = matrix[x][y];
                    int tmp = matrix[cur[0]][cur[1]] + 1;
                    if (value <= tmp)
                        continue;

                    queue.offer(new int[]{x, y});
                    matrix[x][y] = tmp;
                }
            }
        }


        return matrix;
    }

```