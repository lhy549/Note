
使用这种方式写排序的优点和缺点：

	package com.lanhuayan.kuayu.threaddomo;
	
	public class ArraySort implements Runnable{
	    private String num;
	    public ArraySort(int num) {
	        this.num = num +"";
	    }
	    public static void main(String[] args) {
	        int[] arr = {10,2000,654345,2345654,5678876};
	
	        for (int i = 0; i <arr.length ; i++) {
	            new Thread(new ArraySort(arr[i])).start();
	        }
	    }
	    @Override
	    public void run() {
	        try {
	            Thread.sleep(Integer.parseInt(num));
	            System.out.println(num);
	        } catch (InterruptedException e) {
	            e.printStackTrace();
	        }
	    }
	}

虽然也可以实现排序，但是如果数组的数值很大，那么休眠的时间会很久

