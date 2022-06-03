#include<stdio.h>
#include<stdlib.h>
int main()
{
        int row, col= 0, mouse[100][2], cat[1][2], m_count= 0, count= 0, step[100][100]= {0}, input[10000][2], s_row, s_col, ans=10001;
        char alpha, arr[100][100];
        while(1)
        {
                scanf("%d", &row);
                if(row== 0)
                        break;
                alpha= getchar();
                m_count= 0;
                count= 0;
                ans= 10001;
                for(int i= 0; i< row; i++){
                        col= 0;
                        while(1){
                                alpha= getchar();
                                if(alpha!= '\n'){
                                        if(alpha== 'K'){
                                                cat[0][0]= i;
                                                cat[0][1]= col;
                                        }
                                        else if(alpha== '@'){
                                                mouse[m_count][0]= i;
                                                mouse[m_count][1]= col;
                                                m_count++ ;
                                        }

                                        arr[i][col]= alpha;
                                        step[i][col]= 0;
                                        col++ ;
                                }
                                else
                                        break;
                        }
                }

                input[count][0]= cat[0][0];
                input[count++][1]= cat[0][1];
                for(int i= 0; i< count; i++){
                        s_row= input[i][0];
                        s_col= input[i][1];
                        if(arr[s_row- 1][s_col]!= '#'){
                                input[count][0]= s_row- 1;
                                input[count++][1]= s_col;
                                arr[s_row][s_col]= '#';
                                step[s_row- 1][s_col]= step[s_row][s_col]+ 1;
                        }
                        if(arr[s_row+ 1][s_col]!= '#'){
                                input[count][0]= s_row+ 1;
                                input[count++][1]= s_col;
                                arr[s_row][s_col]= '#';
                                step[s_row+ 1][s_col]= step[s_row][s_col]+ 1;
                        }
                        if(arr[s_row][s_col- 1]!= '#'){
                                input[count][0]= s_row;
                                input[count++][1]= s_col- 1;
                                arr[s_row][s_col]= '#';
                                step[s_row][s_col- 1]= step[s_row][s_col]+ 1;
                        }
                        if(arr[s_row][s_col+ 1]!= '#'){
                                input[count][0]= s_row;
                                input[count++][1]= s_col+ 1;
                                arr[s_row][s_col]= '#';
                                step[s_row][s_col+ 1]= step[s_row][s_col]+ 1;
                        }
                }

                for(int i= 0; i< m_count; i++){
                        int tmp= step[mouse[i][0]][mouse[i][1]];
                        if(tmp< ans&& tmp!= 0)
                                ans= tmp;
                }

                if(ans!= 10001)
                        printf("%d\n", ans);
                else
                        printf("= =\"\n");
        }
}
