# 최 근접 쌍 찾기

- ## 2차원 배열을 이용하기

```
import java.util.*;

public class force{
    static int[][] point;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x =sc.nextInt(); // Number of points
        point = new int[x][2]; // The location of each point
        // Enter the location
        for(int i=0; i<x; i++){
            point[i][0]=sc.nextInt(); // x value
            point[i][1]=sc.nextInt(); // y value
        }
        // Finding the distance
        double min = 1000;
        int minX=0;
        int minY=0;
        for(int i=0; i<x-1; i++){
            for(int j=i+1; j<x; j++){
                double temp = calDist(i,j);
                if(temp<min) {
                    min=temp; minX=i; minY=j;
                }
            }
        }
        System.out.println(min+" "+minX+" "+minY);
    }
    public static double calDist(int a, int b){
        return Math.sqrt(Math.pow(point[a][0]-point[b][0],2)+Math.pow(point[a][1]-point[b][1],2));
        //Math.sqrt is a method to find the root.(But I can't understand about the calDist. So I referenced the blog.)
    }
}
```

![텍스트](C:\Users\82104\Desktop.jpg "냥이")







- ## 구조체 이용하기

```
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;

public class comal {

    static Point p[];

    static class Point {
        int x;
        int y;
        Point( int x, int y ) {
            this.x = x;
            this.y = y;
        }
    }

    static int getDistance( Point p1, Point p2 ) {
        return (p1.x-p2.x)*(p1.x-p2.x) + (p1.y-p2.y)*(p1.y-p2.y);
    }

    // (4)
    static int getmin( int left, int right ) {
        int d_min = Integer.MAX_VALUE;
        for( int i = left; i < right; i++ ) {
            for( int j = i+1; j <= right; j++ ) {
                int d = getDistance( p[i], p[j] );
                if( d_min > d ) d_min = d;
            }
        }
        return d_min;
    }

    // (3)
    static int divCon( int left, int right ) {

        // 4
        int size = right - left + 1;	 // section size
        if( size <= 3 )
            return getmin( left, right );

        // 5
        int mid = ( left + right ) / 2;
        int d_s_left = divCon( left, mid );		// left section distance
        int d_s_right = divCon( mid+1, right );	// right section distance

        int d_min = Math.min( d_s_left, d_s_right );

        // 6
        List<Point> s_mid = new ArrayList<>();	// middle section
        for( int i = left; i <= right; i++ ) {
            int d_x = p[i].x - p[mid].x;
            if( d_x * d_x < d_min )
                s_mid.add( p[i] );
        }

        // 7
        Collections.sort( s_mid, ( p1,p2 ) -> p1.y - p2.y );
        int size1 = s_mid.size();   // candidate size
        for( int i = 0; i < size1-1; i++ ) {
            for( int j = i+1; j < size1; j++ ) {
                int d_y = s_mid.get(j).y - s_mid.get(i).y;
                if( d_y * d_y < d_min ) {
                    int d = getDistance( s_mid.get(i), s_mid.get(j) );
                    if( d_min > d ) d_min = d;
                }
                else break;
            }
        }
        return d_min;
    }

    public static void main(String[] args) {

        // 1
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        p = new Point[n];
        for( int i = 0; i < n; i++ )
            p[i] = new Point( sc.nextInt(), sc.nextInt() );
        sc.close();

        // 2
        Arrays.sort( p, ( p1,p2 ) -> p1.x - p2.x );

        // 3
        System.out.println( divCon( 0, n-1 ) );
    }
}
```

