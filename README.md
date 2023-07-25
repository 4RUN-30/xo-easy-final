package com.arunsh;

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/addStudent")
public class StudentService extends HttpServlet{

	public void doPost(HttpServletRequest req,HttpServletResponse res) throws IOException{
		String name = req.getParameter("sname");
		String action = req.getParameter("action");
		if(action.equals("post")) {
			Student s = new Student(name);
			this.addStudent(s);
		}
		PrintWriter pr = res.getWriter();
		pr.println(action);
	} 
	public Student addStudent(Student student){
		try {
			Class.forName("com.mysql.jdbc.Driver");
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school","root","root");
			String sql = "INSERT INTO school.student ('"+student.getName()+"','"+student.getId()+"');";
			PreparedStatement ps = con.prepareStatement(sql);
			ps.executeUpdate();
			ps.close();
			con.close();
		}
		catch(Exception e) {
			
		}
		return student;
	}
	
}
