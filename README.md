# Print_Formatting
CS3 assignment (Dalton)
import java.util.Scanner;
import java.text.*;
import java.math.*;
import java.text.DecimalFormat;
import java.text.NumberFormat;


public class Print_Formatting {

	/**
	 *1. &&&&&&, 456
	 *2. &&&&&&,&, 1000000
	 *3. $&&&&.&&, 123.38
	 *4. &&&.&&&, 23.49
	 *5. &&&.&&&, 23.4999
	 *6. &&&E, 45
	 */

	static String[] section;
	static String[] splitString;
	static String[] splitValue;
	static char[] stemp;
	static char[] ctemp;
	static char[] holder;
	static int value;
	static double d;
	//static 

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int counter = 0;
		//while(counter<=5){
		Scanner scan = new Scanner(System.in);
		String s = scan.nextLine();
		//System.out.println("original input= " + s);
		section = s.split(", ");
		/*for(int i = 0; i<section.length; i++){
			System.out.println("section[" + i + "]= " + section[i]);
		}*/
		String temp;//value to string
		String string;//string to string

		//manipulates the stuff in String
		stemp = section[0].toCharArray();//array of values in string
		string = section[0].toString();//puts all the &s into a string 
		//System.out.println("string= " + string);
		splitString = string.replace(".", ", ").split(", ");
		/*for(int i = 0; i<splitString.length; i++){
			System.out.println("splitString[" + i + "]= " + splitString[i]);
		}*/

		//manipulates the stuff in Value
		ctemp = section[1].toCharArray();//array of numbers in value
		temp = section[1].toString();//puts all the numbers into a string
		//System.out.println("temp= " + temp);
		splitValue = temp.replace(".", ", ").split(", ");
		/*for (int i = 0; i<splitValue.length; i++){
			System.out.println("splitValue[" + i + "]= " + splitValue[i]);
		}*/



		if(temp.contains(".")) {d = Double.parseDouble(temp);}//if value has a decimal make it a double
		else{value = Integer.parseInt(temp);}//if it is an int make it an int

		if(section[0].contains(",")){
			rule2();
		} 
		else if(stemp[0] == '&' && temp.contains(".")){
			if(splitString[1].length()>splitValue[1].length()){
				rule3();
			}
			else{
				rule4();
			}

		}
		else if (stemp[0] == '$'){
			rule5();
		}
		else if (section[0].contains("*$")){
			rule6();
		}
		else if(section[0].contains("E")){
			rule7();
		}
		else{
			rule1();
		}
		//}counter++;
	}//main

	private static void rule1() {
		//System.out.println("rule 1");
		int and = stemp.length;
		int digits = ctemp.length;
		int temp = and-digits;
		while(temp>0){
			System.out.print("*");
			temp--;
		}
		System.out.println(value);
	}

	private static void rule2() {
		//System.out.println("rule 2");
		NumberFormat myFormat = NumberFormat.getInstance();
		myFormat.setGroupingUsed(true);
		System.out.println(myFormat.format(value));
	}

	private static void rule3() {
		//System.out.println("rule 3");
		int stars = splitString[0].length()-splitValue[0].length();//*'s before the value printed
		String splaceholder = "*********************************************************************************************";
		int scounter = splaceholder.length()-stars;
		splaceholder = splaceholder.substring(scounter);
		int zeros = splitString[1].length()-splitValue[1].length();
		String zplaceholder = "000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000";
		int zcounter = zplaceholder.length()-zeros;
		zplaceholder = zplaceholder.substring(zcounter);
		String str = new StringBuilder().append(splaceholder).append(d).append(zplaceholder).toString();
		System.out.println(str);
	}

	private static void rule4() {
		//System.out.println("rule 4");
		int zeros = splitValue[0].length();//# of digits printed before decimal
		String zplaceholder = "000000000000000000000000000000000000000000000000000000000000000000000000000000000000000";
		int zcounter = zplaceholder.length()-zeros;
		zplaceholder = zplaceholder.substring(zcounter);
		//System.out.println(zplaceholder);
		int hashes = splitString[1].length();//# of digits printed after decimal
		String hplaceholder = "############################################################################################";
		int hcounter = hplaceholder.length()-hashes;
		hplaceholder = hplaceholder.substring(hcounter);
		hplaceholder = hplaceholder.replace("#", "0");
		//System.out.println(hplaceholder);
		int stars = splitString[0].length()-splitValue[0].length();//*'s before the value printed
		String splaceholder = "*********************************************************************************************";
		int scounter = splaceholder.length()-stars;
		splaceholder = splaceholder.substring(scounter);
		String str = new StringBuilder().append(zplaceholder).append(".").append(hplaceholder).toString();
		DecimalFormat formatter = new DecimalFormat(str);
		formatter.format(d);
		System.out.print(splaceholder);
		System.out.println(formatter.format(d));
	}

	private static void rule5() {
		//System.out.println("rule 5");
		//System.out.println("double d " + d);
		System.out.println("$" + d + "");
	}

	private static void rule6() {
		//System.out.println("rule 6");
		int and = stemp.length-ctemp.length-2;
		String splaceholder = "*********************************************************************************************";
		int counter = splaceholder.length()-and;
		splaceholder = splaceholder.substring(counter);
		String str = new StringBuilder().append(splaceholder).append('$').append(d).toString();
		System.out.println(str);
	}

	private static void rule7() {
		// System.out.println("rule 7");
		int and = stemp.length-2;
		String zplaceholder = "0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000";
		int counter = zplaceholder.length()-and;
		zplaceholder = zplaceholder.substring(counter);
		String str = new StringBuilder().append("0.").append(zplaceholder).append("E0").toString();
		double d = value + .0;
		DecimalFormat formatter = new DecimalFormat(str);
		System.out.println(formatter.format(d));
	}
	
}//class

