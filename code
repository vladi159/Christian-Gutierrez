using System;

public class Program
{
    public struct Point
    {
        public int x;
        public int y;

        public Point(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    public struct Node
    {
        public Point parent;
        public int dist;

        public Node(Point parent, int dist)
        {
            this.parent = parent;
            this.dist = dist;
        }
    }

    static int ROWS = 10;
    static int COLS = 10;
    static int[][] moves = { new int[] { -1, 0 }, new int[] { 1, 0 }, new int[] { 0, -1 }, new int[] { 0, 1 } };

    static bool IsValid(int x, int y, int[][] maze)
    {
        return x >= 0 && x < ROWS && y >= 0 && y < COLS && maze[x][y] != 1;
    }

    static void PrintPath(Point[] path, int pathLen)
    {
        for (int i = 0; i < pathLen; i++)
        {
            Console.WriteLine($"({path[i].x}, {path[i].y})");
        }
    }

    static void FindShortestPath(int[][] maze, Point start, Point end)
    {
        Node[] queue = new Node[ROWS * COLS];
        bool[,] visited = new bool[ROWS, COLS];
        Point[] path = new Point[ROWS * COLS];
        int front = 0, rear = 0;
        bool found = false;

        for (int i = 0; i < ROWS; i++)
        {
            for (int j = 0; j < COLS; j++)
            {
                visited[i, j] = false;
            }
        }

        queue[rear++] = new Node(start, 0);
        visited[start.x, start.y] = true;

        while (front < rear)
        {
            Node current = queue[front++];

            if (current.parent.x == end.x && current.parent.y == end.y)
            {
                Console.WriteLine("El camino más corto es:");
                Console.WriteLine($"({start.x}, {start.y})");
                PrintPath(path, current.dist);
                found = true;
                break;
            }

            for (int i = 0; i < 4; i++)
            {
                int newX = current.parent.x + moves[i][0];
                int newY = current.parent.y + moves[i][1];

                if (IsValid(newX, newY, maze) && !visited[newX, newY])
                {
                    queue[rear++] = new Node(new Point(newX, newY), current.dist + 1);
                    visited[newX, newY] = true;
                    path[current.dist] = new Point(newX, newY);
                }
            }
        }

        if (!found)
        {
            Console.WriteLine("No hay camino posible desde A hasta B.");
        }
    }

    public static void Main()
    {
        int[][] maze = new int[][]
        {
            new int[] {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
            new int[] {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
            new int[] {0, 0, 0, 1, 0, 0, 0, 1, 0, 0},
            new int[] {0, 0, 0, 1, 0, 0, 0, 1, 0, 'B'},
            new int[] {1, 1, 1, 0, 0, 0, 0, 1, 0, 0},
            new int[] {0, 0, 0, 0, 1, 1, 1, 1, 0, 0},
            new int[] {0, 0, 0, 0, 1, 0, 0, 0, 0, 0},
            new int[] {'A', 0, 0, 0, 1, 0, 0, 0, 0, 0},
            new int[] {0, 0, 0, 0, 1, 0, 0, 0, 0, 0},
            new int[] {0, 0, 0, 0, 1, 0, 0, 0, 0, 0}
        };

        Point start = new Point(7, 0);  // Posición de inicio (A)
        Point end = new Point(3, 9);    // Posición de fin (B)

        FindShortestPath(maze, start, end);

        Console.WriteLine("Presiona Enter para salir...");
        Console.ReadLine();
    }
}
