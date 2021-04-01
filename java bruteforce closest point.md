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