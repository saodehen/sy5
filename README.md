实验目的：
分析学生选课系统
使用GUI窗体及其组件设计窗体界面
完成学生选课过程业务逻辑编程
基于文件保存并读取数据
处理异常


实验要求：
一、系统角色分析及类设计
例如：学校有“人员”，分为“教师”和“学生”，教师教授“课程”，学生选择课程。
定义每种角色人员的属性，及其操作方法。
属性示例：	人员（编号、姓名、性别……）
教师（编号、姓名、性别、所授课程、……）
			学生（编号、姓名、性别、所选课程、……）
			课程（编号、课程名称、上课地点、时间、授课教师、……）
以上属性仅为示例，同学们可以自行扩展。

二、要求:
1、设计GUI窗体，支持学生注册、课程新加、学生选课、学生退课、打印学生选课列表等操作。
2、基于事件模型对业务逻辑编程，实现在界面上支持上述操作。
3、针对操作过程中可能会出现的各种异常，做异常处理
4、基于输入/输出编程，支持学生、课程、教师等数据的读写操作。
5、基于Github.com提交实验，包括实验SRC源文件夹程序、README.MD实验报告文档。
核心代码：


测试类
```java
     public class StudentManagementSystem {
    	public static void main(String[] args) {
		  new LoginFrame();
	}
}
```
学生类
  
     public class Course {
	private String cno;
	private String cname;
	private String cnum;
	private String dept;
	private String teacher;
	
      }
添加课程
 
        public void insert() { 
		 String cno = tcno.getText();
		String cname = tcname.getText();
        String cnum = tcredit.getText();
		String dept = cbcdept.getSelectedItem().toString();
		String teacher = ttname.getText();
		if(cno.equals("")||cname.equals("")||teacher.equals("")||cnum.equals("")){
			JOptionPane.showMessageDialog(null, "课程号、课程名、学分数、授课教师不能有空值！");
		}else{
			Course can = new Course();
			can.setCno(cno);
			can.setCname(cname);
			can.setCnum(cnum);
			can.setDept(dept);
			can.setTeacher(teacher);
			 String fileUrl1= "./files/course.txt";
			String fileUrl2= "./files/"+"*"+"/kexuan.txt";
			FileUtil.FileExistTest(fileUrl1);
			FileUtil.FileExistTest(fileUrl2);
			
			Boolean flag1 = FileUtil.addSelected(can,fileUrl1);
			        Boolean flag2 = FileUtil.addSelected(can,fileUrl2);
			  if (flag1==true) {
				JOptionPane.showMessageDialog(null, "增加成功！");
				listener.refreshUI();
				setVisible(false);
			}
		
				
		}
    
    选课写入

      public void getNotSelected(){

		String fileUrl= "./files/"+LoginFrame.loginName+"/kexuan.txt";
		FileUtil.FileExistTest(fileUrl);
		ArrayList<Course> notSelectedCourceList = FileUtil.getNotSelectedCource(fileUrl);
		valuesNotSelected = new Object[notSelectedCourceList.size()][5];
		for (int i = 0; i < notSelectedCourceList.size(); i++) {
			valuesNotSelected[i][0] = notSelectedCourceList.get(i).getCno();
			valuesNotSelected[i][1] = notSelectedCourceList.get(i).getCname();
			valuesNotSelected[i][2] = notSelectedCourceList.get(i).getCnum();
			valuesNotSelected[i][3] = notSelectedCourceList.get(i).getDept();
			valuesNotSelected[i][4] = notSelectedCourceList.get(i).getTeacher();;
		}
	}
  
  退课 
  
      public void dropCourse(){
		int rowNotSelected = -1,rowSelected=-1;
		 rowNotSelected = tableNotSelected.getSelectedRow();
		rowSelected =tableSelected.getSelectedRow();
		if (rowNotSelected == -1 && rowSelected == -1) {
			JOptionPane.showMessageDialog(null, "请选择要退的课程！");
		} else if(rowNotSelected != -1 && rowSelected == -1){
			JOptionPane.showMessageDialog(null, "您未选修此课程，请重新选择！");
		}else{
			String cno=valuesSelected[rowSelected][0].toString();
			String cname=valuesSelected[rowSelected][1].toString();
			String cnum=valuesSelected[rowSelected][2].toString();
			String dept=valuesSelected[rowSelected][3].toString();
			String teacher=valuesSelected[rowSelected][4].toString();
			Course can = new Course();
			can.setCno(cno);
			can.setCname(cname);
			can.setCnum(cnum);
			can.setDept(dept);
			can.setTeacher(teacher);
			
			String fileUrl1= "./files/"+LoginFrame.loginName+"/kexuan.txt";
			Boolean flag2 = FileUtil.addSelected(can,fileUrl1);
			FileUtil.FileExistTest(fileUrl1);
			
			String fileUrl2= "./files/"+LoginFrame.loginName+"/yixuan.txt";
			FileUtil.FileExistTest(fileUrl2);
			Boolean flag1 = FileUtil.removeNotSelected(can,fileUrl2);
			if (flag1==true&&flag2==true) {
				JOptionPane.showMessageDialog(null, "退课成功！");
				refresh();
			}
		}
	}
  
 流程图
 ===============

![]()
  
 结果图
 ================
   
![]()
![]() 
![]()
![]()



实验心得：
 学习Java，信心，恒心，毅力是最重要的。这是我们必须具备的心理素质。要是学习这门语言开始的时候很有兴趣，遇到苦难就退缩，
 这样最终会放弃学习java，没有经历风雨怎么见彩虹。编程就是有的时候就是那么这么人。会遇到很多的困惑。但是一旦你
 弄懂了，或者是你把问题解决了，你会感到很兴奋，编程的快乐就在此 了。多看看一些资料，多多的向高手请教，这样才好。
 要学会总结和领会，当然，学习java一个人有一个人的想法，也有自己的独特学习方法。总之适合自己的就是最好的。

 
