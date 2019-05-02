package com.capgemini.contactbook.ui;

import java.util.Scanner;

import com.capgemini.contactbook.bean.EnquiryBean;
import com.capgemini.contactbook.exception.ContactBookException;
import com.capgemini.contactbook.service.ContactBookServiceImpl;
import com.capgemini.contactbook.service.IContactBookService;

public class Client {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Scanner sc=new Scanner(System.in);
		
	
		
	IContactBookService icb=new ContactBookServiceImpl();
	
	
	do {
		System.out.println("Menu");
		System.out.println("1.Enter enquiry details");
		System.out.println("2.view enquiry details on id");
		System.out.println("3.exit");

		
		int choice = sc.nextInt();
		switch(choice)
		{
		case 1:System.out.println("enter first name");
		String fname=sc.next();
		System.out.println("enter last name");
		String lname=sc.next();
		System.out.println("enter contact number");
		String cno=sc.next();
		System.out.println("enter preferred domain");
		String pd=sc.next();
		System.out.println("enter prferred location");
		String pl=sc.next();
		
		EnquiryBean e=new EnquiryBean(0,fname,lname,cno,pd,pl);
		
			try {
				if(icb.isValidEnquiry(e))
				{
					icb.addEnquiry(e);
					System.out.println("Thank you for shopping with us"+e.getEnqryId());
				}
			} catch (ContactBookException e1) {
				// TODO Auto-generated catch block
				System.err.println("not valid entry");
			}
			break;
		case 2:
			System.out.println("enter the enquiry no.");
			int eid =sc.nextInt();
			try {
				icb.getEnquiryDetails(eid);
			} catch (ContactBookException e1) {
				System.err.println("enquiry details not exist ");
			}
			
			
			break;
			
			
		case 3:System.exit(0);
		default: System.out.println("Invalid Choice try again");
		
		
	}
	
	}while(true);
	
}
}
