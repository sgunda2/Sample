
package com.ssdi;

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.PreparedStatement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;


@WebServlet("/StudentInfo")
public class StudentInfo extends HttpServlet {
	private static final long serialVersionUID = 1L;
        static Connection con=null;
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException
     	{
		response.setContentType("text/html");
	   PrintWriter pw=response.getWriter();
	   try{
		   this.makeConnection();
		   PreparedStatement ps=con.prepareStatement("select * from STUDENT");
		   ResultSet rs=ps.executeQuery();
		   
		   pw.println("<table border='1'>");
		   while(rs.next())
		   {
			   pw.println("<tr>");
			   
			   pw.println("<td>"+rs.getString(1)+"</td>");
			   pw.println("<td>"+rs.getString(2)+"</td>");
			   
			   pw.println("</tr>");
			   }
		      pw.println("</table>");
		    }
	   catch(Exception e)
	   {
		   System.out.println("Error"+e);
	   }finally
		{
			pw.close();}
     }
     
     public void makeConnection()
     {
    	try{
    	Class.forName("com.mysql.jdbc.Driver");
    	con=DriverManager.getConnection("jdbc:mysql://localhost/ssdi", "ssdi", "ssdi");
    	}catch(Exception e)
    	{
    		System.out.println("Error.... "+e);
    	}
     }
      }


