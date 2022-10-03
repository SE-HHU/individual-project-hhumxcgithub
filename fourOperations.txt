import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Random;
import java.util.Scanner;

public class fourOperation {
    public static void main(String[] args) {
        /*编写一个四则运算程序,100以内加减法,使用参数控制生成题目的个数,
        每道题目中出现的运算符不超过两个,一次运行中生成的题目不能重复,生成题目的同时,
        计算出所有题目的答案,并存入执行程序的当前目录下的文件中*/
        Random r = new Random();
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入需要的题目数量:");
        int count = sc.nextInt();//键盘录入需要生成的题目个数
        int[] arr1 = new int[count];//定义数组储存题目的答案,若答案存在重复,则题目一定重复.
        String[] arr2 = new String[count];//定义数组储存题目
        boolean flag = true;//定义标识,若生成的题目不重复,则将flag变为false,若重复,则flag任为true,继续执行while,重新生成题目
        //while循环反复生成题目,直到生成的题目答案不相同,答案不相同可推出题目一定不相同
        while (flag) {
            //通过for循环产生指定个数题目
            for (int i = 0; i < count; i++) {
                int number1 = r.nextInt(101);//生成0~100间的随机数
                int number2 = r.nextInt(101);
                int number3 = r.nextInt(101);
                int operators = r.nextInt(2) + 1;//用于判断用一个或两个运算符
                int as1 = r.nextInt(2);//用于判断用+或-运算符,0为+,1为-
                int as2 = r.nextInt(2);//用于判断用+或-运算符
                int answer;
                String exercise;
                //通过if选择结构产生不同要求的题目
                if (operators == 1 && as1 == 0) {
                    exercise = number1 + "+" + number2 + "=";
                    answer = number1 + number2;
                } else if (operators == 1 && as1 == 1) {
                    exercise = number1 + "-" + number2 + "=";
                    answer = number1 - number2;
                } else if (operators == 2 && as1 == 0 && as2 == 0) {
                    exercise = number1 + "+" + number2 + "+" + number3 + "=";
                    answer = number1 + number2 + number3;
                } else if (operators == 2 && as1 == 0 && as2 == 1) {
                    exercise = number1 + "+" + number2 + "-" + number3 + "=";
                    answer = number1 + number2 - number3;
                } else if (operators == 2 && as1 == 1 && as2 == 0) {
                    exercise = number1 + "-" + number2 + "+" + number3 + "=";
                    answer = number1 - number2 + number3;
                } else {
                    exercise = number1 + "-" + number2 + "-" + number3 + "=";
                    answer = number1 - number2 - number3;
                }
                arr1[i] = answer;//每次生成题目后,将答案存入数组
                arr2[i] = exercise;//题目存入数组
            }
            flag = false;//while执行一次,将flag变为false,若下面for循环中检测有重复答案,则flag变为true,重新执行while循环
            //for循环检测数组中元素是否有重复
            for (int i = 0; i < arr1.length; i++) {
                for (int j = i+1; j < arr1.length; j++) {
                    if (arr1[i] == arr1[j]){
                        flag = true;
                        break;
                    }
                }
                if (flag){
                    break;
                }
            }
        }
        //for循环遍历数组元素,得到题目和答案
        for (int i = 0; i < arr1.length; i++) {
            System.out.println((i+1) + "." + " " + arr2[i] + arr1[i]);
        }
        //将题目写入文件exercises.txt
        try {
            File file1 = new File("C:\\Users\\1744355801\\java作业\\exercises.txt");
            if (!file1.exists()){
                file1.createNewFile();
            }
            FileWriter fw = new FileWriter(file1.getAbsoluteFile());
            BufferedWriter bw = new BufferedWriter(fw);
            for (int i = 0; i < arr2.length; i++) {
                bw.write((i+1) + "." + '\t' + arr2[i] + '\n');
            }
            bw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        //将答案写入文件answers.txt
        try {
            File file2 = new File("C:\\Users\\1744355801\\java作业\\answers.txt");
            if (!file2.exists()){
                file2.createNewFile();
            }
            FileWriter fw = new FileWriter(file2.getAbsoluteFile());
            BufferedWriter bw = new BufferedWriter(fw);
            for (int i = 0; i < arr1.length; i++) {
                bw.write( (i+1) + "." + '\t' + arr1[i] + '\n');//写入整数类型数据会得到乱码文件
            }
            bw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}