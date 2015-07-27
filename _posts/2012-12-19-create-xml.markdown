---
author: fangrenbin
comments: true
date: 2012-12-19 14:28:48+00:00
layout: post
slug: create-xml
title: dom4j创建xml文件
wordpress_id: 405
categories:
- xml
tag:
- dom4j
- java
- xml
- 创建xml
- 生成xml
---

把数据输出成一个xml文件，写了一个小例子，做笔记参考。
流程就是创建document对象，然后增加节点，设置节点值，设置节点属性，然后再输出文件。

    
    
    package name.frb.xml;
    
    import java.io.File;
    import java.io.FileWriter;
    import java.io.IOException;
    import java.util.Random;
    
    import org.dom4j.Document;
    import org.dom4j.DocumentException;
    import org.dom4j.DocumentHelper;
    import org.dom4j.Element;
    import org.dom4j.io.OutputFormat;
    import org.dom4j.io.XMLWriter;
    
    public class XmlDemo {
    	public static void main(String args[]) throws DocumentException {
    		String file = "src/main/java/student.xml";
    
    		String[] studentName = { "小白", "小司", "小宝" };
    		String[] courseName = { "数学", "英语", "美术", "体育" };
    
    		XmlDemo xmlDemo = new XmlDemo();
    		xmlDemo.buildXml(file, studentName, courseName);
    		System.out.println("-------创建xml完成!-------");
    	}
    
    	/**
    	 * 创建xml文件
    	 *
    	 * @param fileName
    	 *            文件名称
    	 * @param studentName
    	 *            学生姓名
    	 * @param courseName
    	 *            　课程名称
    	 */
    	private void buildXml(String fileName, String[] studentName,
    			String[] courseName) {
    		Document doc = DocumentHelper.createDocument();
    
    		// 增加节点
    		Element root = doc.addElement("Root");
    		Element headNode = root.addElement("Head");
    		Element bodyNode = root.addElement("Body");
    
    		// 增加节点并设置节点内容
    		Element codeEle = headNode.addElement("Code");
    		codeEle.setText("09013044e126");
    		Element examEle = headNode.addElement("Exam");
    		examEle.setText("True");
    
    		// 增加节点内容
    		addCourseList(bodyNode, studentName, courseName);
    		try {
    			// 文件输出对象
    			FileWriter fileWriter = new FileWriter(new File(fileName));
    
    			// xml输出格式
    			OutputFormat xmlFormat = OutputFormat.createPrettyPrint();
    			xmlFormat.setEncoding("gbk");
    
    			// xml文件输出对象
    			XMLWriter xmlWriter = new XMLWriter(fileWriter, xmlFormat);
    
    			xmlWriter.write(doc);
    			xmlWriter.close();
    		} catch (IOException e) {
    			e.printStackTrace();
    		}
    	}
    
    	/**
    	 * 创建课程list
    	 *
    	 * @param bodyEle
    	 *            body Element
    	 * @param studentName
    	 *            学生名字
    	 * @param courseName
    	 *            　课程名称
    	 */
    	private void addCourseList(Element bodyEle, String[] studentName,
    			String[] courseName) {
    		Element bodyNode = bodyEle.addElement("CourseList");
    		for (int i = 0; i < studentName.length; i++) {
    			Element courseList = bodyNode.addElement("Course");
    			courseList.setText(courseName[i]);
    			addStudents(bodyNode, studentName);
    		}
    	}
    
    	/**
    	 * 创建学生list
    	 *
    	 * @param courseList
    	 *            课程list
    	 * @param studentName
    	 *            学生名称
    	 */
    	private void addStudents(Element courseList, String[] studentName) {
    		Element student = courseList.addElement("Student");
    		for (int i = 0; i < studentName.length; i++) {
    			Element studentNode = student.addElement("StudentName");
    			studentNode.setAttributeValue("score", new Random().nextInt(100)
    					+ "");
    			studentNode.setText(studentName[i]);
    		}
    	}
    }
