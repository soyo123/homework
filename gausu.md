//  main.cpp
//  gausu
//  Created by 洋曹 on 2018/6/2.
//  名前：曹洋　学修番号：18861604
//ガウス消去
#include<stdio.h>
#include<math.h>

#define N 5
int main()
{
    int i, j, k, l;
    double a[N][N] = {{1,2,3,4,5},{2,3,4,5,1},{3,4,-5,1,2},{4,5,1,2,3},{5,1,2,3,4}},
    b[N] = {1,2,4,8,16}, h[N];
    double sa, s;
    for(k = 0; k < N-1; k++){
        l = k;
        sa = fabs( a[k][k] );
        for(i = k+1; i < N; i++){
            if(fabs( a[i][k] ) > sa){
                l = i;
                sa = fabs( a[i][k] );
            }
        }
        
        
        if(fabs( sa ) < 1.0e-12){
            printf("too small pivot! \n");
            return(0);
        }
        if(l != k){
            for(i = k; i < N; i++){
                
                s = a[k][i];
                a[k][i] = a[l][i];
                a[l][i] = s;
            }
        
            s = b[k];
            b[k] = b[l];
            b[l] = s;
        }
        /* 前進消去 */
        for(i = k +1; i < N; i++){
            h[i] = a[i][k] / a[k][k];
            a[i][k] = 0.0;
            /* 第ｋ行を倍して、第ｉ行に加える */
            for(j = k + 1; j < N; j++){
                a[i][j] = a[i][j] - a[k][j] * h[i];
            }
            b[i] = b[i] - b[k] * h[i];
        }
    }
    /* 後退代入 */
    for(i = N - 1; i >= 0; i--){
        for(j = i + 1; j < N; j++){
            b[i] = b[i] - a[i][j] * b[j];
            a[i][j] = 0.0;
        }
        b[i] = b[i] / a[i][i];
        a[i][i] = 1.0;
    }
    for(i = 0; i < N; i++){
        printf("x[%2d] = %12.8lf\n",i+1,b[i]);
    }
    return(0);
}
