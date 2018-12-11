# Colatz-fun
If you throw enough computing power at a problem you can almost accomplish something
source code :
import java.util.*;
import java.io.*;
public class Control 
{
    Arraylist data;
    public void main(int run) throws IOException
    {
        // PrintStream out = new PrintStream(new FileOutputStream("Output.txt"));
        data = new Arraylist(0);
        long temp;
        int runs = 0;
        boolean flag = false;
        for(int i = 1; i < run; i+=2)
        {
            temp = i;
            while(!flag)
            {
                if(temp == 1){
                    flag = true;
                    // System.out.println(i+" , "+flag+" , "+runs);
                }
                if(temp % 2 == 1){
                    temp = (temp * 3) + 1;
                    //out.println("up "+ temp);
                }else
                {
                    temp = temp / 2;
                    //out.println("down "+ temp);
                }
                // if(runs > 500){
                    // out.println("ERROR "+ temp);
                    // return;
                // }
                runs++;
            }
            flag = data.findIter(runs);
            if(!flag){
                data.add(runs);
            }
            flag = false;
            runs = 0;
        }
        // out.close();
        PrintStream rout = new PrintStream(new FileOutputStream("Runs.txt"));
        int tango[][] = data.getPlain();
        for(int i = 0; i < data.length; i++)
        {
            rout.println(tango[i][0] +" , "+ tango[i][1]);
        }
        rout.close();
        System.out.println("fin");
    }
}
Custom data structure

public class Arraylist
{
    public int length;
    public int maxNum;
    public int iter[];
    public int midpnt;
    private Cell root;
    private Cell mid;
    private Cell tail;
    public Arraylist(int chad)
    {
        maxNum = chad;
        root = new Cell(chad);
        mid = root;
        tail = root;
        length = 1;
    }
    public void add(int chad)
    {   
        Cell temp;
        if(chad > maxNum){
            maxNum = chad;
            temp = tail;
            temp.setNext(chad);
            tail = temp.next();
            length++;
            midpnt = (int)maxNum/2;
            while((mid.num < midpnt) && (mid.next().num <= midpnt))
            {
                mid = mid.next();
            }
            return;
        }
        else if(chad > midpnt){
            temp = mid;
            while(chad > temp.next().num)
            {
                temp = temp.next();
            }
            temp.setNext(new Cell(chad, temp.next()));
            length++;
            return;
        }
        else{
            temp = root;
            while(chad > temp.next().num)
            {
                temp = temp.next();
            }
            temp.setNext(new Cell(chad, temp.next()));
            length++;
            return;
        }
    }
    // public boolean remove(int bad)
    // {
        // Cell pointer = root;
        // if(pointer.num == bad){
            // root = root.next();
            // length--;
            // return true;
        // }
        // for(int i =1; i <= length; i++)
        // {
            // if(pointer.next() == null){
                // return false;
            // }
            // else if(pointer.next().num == bad){
                // pointer.setNext(pointer.next().next());
                // length--;
                // return true;
            // }
        // }
        // return false;
    // }
    public int findSet(int value, int chad)
    {
        Cell temp = root;
        int ret;
        for(int i = 0; i < length; i++)
        {
            if(temp.num == value)
            {
                ret = temp.num;
                temp.set(chad);
                return ret;
            }
            temp = temp.next();
        }
        return -1;
    }
    public boolean findIter(int value)
    {
        Cell temp =root;
        for(int i = 0; i < length; i++)
        {
            if(temp.num == value)
            {
                temp.iter();
                return true;
            }
            temp = temp.next();
        }
        return false;
    }
    public int[][] getPlain()
    {
        int ret[][] = new int[length][2];
        Cell temp = root; 
        for(int i = 0; i < length; i++)
        {
            ret[i][0] = temp.num;
            ret[i][1] = temp.iter;
            temp =temp.next();
        }
        return ret;
    }
}
class Cell
{
    public int num;
    public int iter;
    public Cell nCell;
    public Cell(int hold)
    {
        num = hold;
        iter= 1;
    }
    public Cell(int hold, Cell next)
    {
        num = hold;
        iter = 1;
        nCell = next;
    }
    public Cell next()
    {
        return nCell;
    }
    public void set(int chad)
    {
        num = chad;
    }
    public void setNext(int chad)
    {
        nCell = new Cell(chad);
    }
    public void setNext(Cell chad)
    {
        nCell = chad;
    }
    public void iter()
    {
        iter++;
    }
    // public abstract void sortByNum();
    // public abstract void sortByIter();
}
