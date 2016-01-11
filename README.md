# projectss
my project repo

<<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.Connection"%>
<html>
    <body>
        <%
            try {
                int r = Integer.parseInt(request.getParameter("r"));
                String n = request.getParameter("n");
                String c = request.getParameter("c");

                String bg = request.getParameter("bg");
                Class.forName("oracle.jdbc.OracleDriver");
                Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");
                PreparedStatement ps = cn.prepareStatement("insert into pres values(?,?,?,?)");
                ps.setInt(1, r);
                ps.setString(2, n);
                ps.setString(3, c);

                ps.setString(4, bg);
//            out.println("<b style='color:#00dd22; font-family:cursive; font-size: 65px;' Registered Successfully </b>");

                ps.executeUpdate();
                response.sendRedirect("p.jsp?a=abc");
                ps.close();
                cn.close();

            } catch (Exception e) {
                response.sendRedirect("p.jsp?err=abc");

            }
        %>
    </body>
</html>


<html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <div id="left">
                        
                        <br><br>

                        <center>
                            <p style="color:red; font-size:30pt;font-family: Monotype Corsiva;font-weight:bolder">About Us</p>
                            
                            <p style="font-family: BOOKMAN OLD STYLE; font-size:15pt; color:white; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; We at Online OPD are providing you Online solutions <br>  <br>for OPD. The idea is to reduce the waiting time in the&nbsp;&nbsp; OPDs&nbsp;&nbsp; and  <br><br>&nbsp;&nbsp;&nbsp;streamline the rush for out-patient consultations. &nbsp;The system    &nbsp;&nbsp;  <br><br> allows patients to view online their waiting time and the availability<br><br> of doctors and visit the OPD accordingly.</p>
                        </center>
                    </div>
                        <div id="right">
                            <center>
                                <br><br><br><br><br><br><br><br>
                            <img src="Photo/us.png">
                            </center>
                        </div>
                    </div>
                </div>
            </body>
        </html>

     
        <<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.Connection"%>
<html>
     <head>
        <title>testing....</title>
        <link href="style.css" rel="stylesheet">
    </head>
    <body>
        <jsp:includepage="header.jsp"/>
                  
            </div>
            <div id="body">
                
                 <jsp:includepage="Menu.jsp"/>
                     
                
                     <div id="content">
                <center>
                    <br><br><br>
        
        <%
            int r = Integer.parseInt(request.getParameter("r"));
            String n = request.getParameter("n");
            int a = Integer.parseInt(request.getParameter("a"));
            String dia = request.getParameter("dia"); 
            String d = request.getParameter("d");
            String m = request.getParameter("m");
            Class.forName("oracle.jdbc.OracleDriver");
            Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");
            PreparedStatement ps = cn.prepareStatement("insert into icard values(?,?,?,?,?,?)");
            ps.setInt(1, r);
            ps.setString(2, n);
            ps.setInt(3, a);
            ps.setString(4, dia);
            ps.setString(5, d);
            ps.setString(6, m);
            out.println("<b style='color:#00dd22; font-family:cursive; font-size: 65px;'> Registered Successfully </b>");
            out.println("\n <a href='fill.jsp;'>Click here to get your ICard</a>");
            ps.executeUpdate();
            ps.close();
            cn.close();
        %>
          
        </div></center>
    </body>
</html>


<html>
    <head>
        <link href="style.css" rel="stylesheet">

        <script>


            function isNumber(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if (charCode > 31 && (charCode < 48 || charCode > 57)) {
                    return false;
                }
                return true;
            }




            function ValidateAlpha(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode < 65 || charCode > 90) && (charCode < 97 || charCode > 123) && charCode !== 32) {
                    return false;
                }
                return true;
            }

        </script>

    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br><br>

                        <center>
                            <h1 style="color:#00dd22; font-family: cursive; font-size:25pt;"><u> Check Patient Status</u></h1><br>
                            <form action="Status.jsp" method="post">
                                <table style="color:yellow; font-weight: bold; font-size:25pt;">
                                    <tr>
                                        <td>Registration No                     </td>
                                        <td><input type="text" name="r" required placeholder="Enter Registration No" onkeypress="return isNumber(event)"></td>

                                    </tr>

                                    <tr>
                                        <td>Name                    </td>
                                        <td><input type="text" name="n" required placeholder="Enter Registered Name" onkeypress="return ValidateAlpha(event)"></td>

                                    </tr>

                                </table>
                                <br><br>
                                <input type="image" src="Photo/submit1.png">
                            </form>
                            <% if (request.getParameter("err") != null) {%>
                            <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22">Credentials does not match.. Please try again with correct credentials</p>
                            <%

                                }%>
                        </center>
                    </div>
                </div>
            </body>
        </html>
        
          
        <% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Doctor"))){ %>


<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br>

                        <center>
                            <%
                                String regno = request.getParameter("v");
                                Class.forName(
                                        "oracle.jdbc.OracleDriver");
                                Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

                                PreparedStatement ps1 = cn.prepareStatement("update patient set status='Closed' where regno=?");

                                ps1.setString(1, regno);
                                ps1.executeUpdate();


                            %>

                            <br>
                            <center><p style='color:#00dd22;font-family: cursive; font-size:20pt;'>Case &nbsp <%=regno%> &nbsp;Closed..  </p></center>










                        </center>

                    </div>

                </div>
                <%                    cn.close();
                %>
            </body>
        </html>

<% } %>


<% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Doctor"))){ %>


<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br>

                        <center>
                            <%
                                String doc=(String)session.getAttribute("uid");
                                Class.forName(
                                        "oracle.jdbc.OracleDriver");
                                Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

                                PreparedStatement ps1 = cn.prepareStatement("select regno, name, age, status from patient where Doc=? AND STATUS='Closed' order by regno");

                                ps1.setString(1,doc);
                                ResultSet rs = ps1.executeQuery();


                            %>

                            <center><p style='color:red;font-family: cursive; font-size:20pt;'><u>Closed Cases </u></p></center>

                            <center>
                                <form action="Doctor.jsp">
                                    <table style="border:5px solid cyan">

                                        <tr>
                                            <td width="120px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Reg No </p></center></td>
                                        <td width="200px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Name </p></center></td>
                                        <td width="50px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Age </p></center></td>
                                        <td width="100px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Status </p></center></td>
                                        
                                        </tr>
                                        <%      while (rs.next()) {
                                                String regno = rs.getString(1);
                                                String name = rs.getString(2);
                                                String age = rs.getString(3);
                                                String status = rs.getString(4);%>
                                        <tr>
                                            <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=regno%> </p></center></td>
                                        <td width="100px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=name%> </p></center></td>
                                        <td width="50px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=age%> </p></center></td>
                                        <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=status%> </p></center></td>

                                        

                                            </tr>






                                            <%} %>



                                    </table>
                                    <br>



                                    <input type=submit value="Back">
                                </form>


                            </center>

                    </div>

                </div>
                <%

                    cn.close();
                %>
            </body>
        </html>
<% } %>


<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>


<%
    String r = (String) session.getAttribute("REG");
    
    Class.forName("oracle.jdbc.OracleDriver");
    Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");
    
    PreparedStatement ps1 = cn.prepareStatement("select name,doc,status,diagnosis from patient where regno=?");
    
    ps1.setString(1, r);
    ResultSet rs = ps1.executeQuery();
    rs.next();
    String name = rs.getString(1);
    String doc = rs.getString(2);
    String status = rs.getString(3);
    String diagnosis=rs.getString(4);
    
 
    
  

%>


<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">


                        <center>
                            <h1 style="color:skyblue; font-family: cursive; font-size:34pt;"><u>Current Status</u> </h1>
                            <br>
                            <table style="border:8px solid cyan">

                                <tr>
                                    <td width="250px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Registration No</p></center></td>
                                <td width="300px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:red"><%=r%> </p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Name </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:red"> <%=name%></p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Doctor </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:orange"> <%=doc%> </p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Diagnosed with </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:orange"> <%=diagnosis%> </p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Status </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:#00dd22"> <%=status%> </p></center></td>
                                </tr>

                              
                               
                            </table>
                            <br>
                            <a href="CheckStatus.jsp"> <img src="Photo/back.jpg"></a>
                        </center>
                    </div>
                </div>
            </body>
        </html>
<%}
        <%
            
                
            session.removeAttribute("REG");
            ps1.close();
            rs.close();
            cn.close();
          
        %>
        
        <html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                        <br><br><img src="Photo/10.jpg" align="left" width="500" height="450">
                             <center>
                        <table border="20" width="500" align="right" color="Pink">
                            <br><br><br>
                            
                            
                            <tr>
                                <td>
                        <p style="font-family:Bookman Old Style;font-weight:bold; font-size:14pt; color:orange"> Hospital Address: Street 1, Lucknow, India</p><br>
                                </td>
                            </tr>
                            <tr>
                                <td>
                        <p style="font-family:Bookman Old Style;font-weight:bold; font-size:14pt; color:orange"> Toll-free: 1800 22 1822</p><br>
                                </td>
                            </tr>
                            <tr>
                                <td>
                        <p style="font-family:Bookman Old Style;font-weight:bold; font-size:14pt; color:orange"> Email: care@OnlineOPD.com</p><br>
                                </td>
                            </tr>
                        </table>
                        </center>
                        

                    </div>
                </div>

            </body>
        </html>
        
        <%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>


<%
    String r = (String) session.getAttribute("PatientReg");

    Class.forName("oracle.jdbc.OracleDriver");
    Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

    PreparedStatement ps1 = cn.prepareStatement("select name,doc,status,diagnosis from patient where regno=?");

    ps1.setString(1, r);
    ResultSet rs = ps1.executeQuery();
    rs.next();
    String name = rs.getString(1);
    String doc = rs.getString(2);
    String status = rs.getString(3);
    String diagnosis = rs.getString(4);
    if (status.equals("Closed")) {
        session.setAttribute("REG", r);
        response.sendRedirect("ClosedStatusPatients.jsp");
    }

    PreparedStatement ps2 = cn.prepareStatement("select count(*) from patient where doc=? and status=?");
    ps2.setString(1, doc);
    ps2.setString(2, "Open");
    ResultSet rs1 = ps2.executeQuery();
    rs1.next();
    String total = rs1.getString(1);

    int i = 0;
    PreparedStatement ps3 = cn.prepareStatement("select regno from patient where doc=? and status=? order by regno");
    ps3.setString(1, doc);
    ps3.setString(2, "Open");
    ResultSet rs2 = ps3.executeQuery();
    while (rs2.next()) {
        i++;
        String position;
        String reg = rs2.getString(1);
        if (reg.equals(r)) {
            if (i == 1) {
                position = "It's your turn now, Visit the Hospital Immediately";
            } else if (i == 2) {
                position = "Your turn is next! Reach hospital on time";
            } else {

                position =  i+"";
            }

%>


<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">


                        <center>
                            <h1 style="color:skyblue; font-family: cursive; font-size:24pt;"><u>Current Status</u> </h1>
                            <br>
                            <table style="border:5px solid cyan">

                                <tr>
                                    <td width="250px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Registration No</p></center></td>
                                <td width="300px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:red"><%=r%> </p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Name </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:red"> <%=name%></p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Doctor </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:orange"> <%=doc%> </p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Diagnosed with </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:orange"> <%=diagnosis%> </p></center></td>
                                </tr>

                                <tr>

                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Status </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:#00dd22"> <%=status%> </p></center></td>
                                </tr>

                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Patients in Queue </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:orange"> <%=total%></p></center></td>
                                </tr>
                                <tr>
                                    <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Your Position </p></center></td>
                                <td><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:#00dd22"> <%=position%> </p></center></td>
                                </tr>
                            </table>
                            <br>
                           
                           <% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Doctor"))){ %>
<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>
    
    <body>
       <jsp:includepage="header.jsp"/>
        <div id="body">
            <jsp:includepage="Menu.jsp"/>
                

            <div id="content">
                <br><br>
                
                <center>
                    <h1 style="color:#00dd22; font-family: cursive; font-size:30pt;"><i> Welcome! <%out.println(" "+session.getAttribute("uid"));%></i></h1><br>
                    <img src="Photo/do.jpg">
                    </center>
            </div>
        </div>
    </body>
</html>
<% }

 %>
 
 <html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        
                        
                        <center>
                        <p style="font-family:Bookman Old Style; font-size:30pt; color:orange"> Features </p>
                        </center>
                        <p style="font-family:Bookman Old Style; font-size:16pt; color:#00dd22; "><i>
                          &nbsp;&nbsp;   1. The patient has to register himself by visiting hospital in order to use the facilities of Online OPD.<br><br>
                         &nbsp;&nbsp;2. The patient will be provided with Unique Registration number.<br><br>
                         &nbsp;&nbsp;3. The patient can view the queue status in real-time using his unique registration number and can visit the   <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; OPD accordingly.<br><br>
                         &nbsp;&nbsp;4. After doctor visits the patient, the status will be closed by respective doctor.<br><br>
                         &nbsp;&nbsp;5. For next visit, one has to go himself again with the registration process.
                         <br><br><br>
                         &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbps;-The OPD Team
                         </i></p>
                        

                    </div>
                </div>

            </body>
        </html>
        
        <html>
    <head>
        <title>testing....</title>
        <link href="style.css" rel="stylesheet">
    </head>
    <body>
       
        
        <jsp:includepage="header.jsp"/>
           
                 
                  
            </div>
            <div id="body">
                 <jsp:includepage="Menu.jsp"/>
                <div id="content">
                
                
                <center>
                    <br>
                    <h1 style="color:#00dd22; font-family: Annabel Script; font-size:25pt;"><i>Registration for ICard </i> </h1>
                  
                    <div id="left">
                       
                    <h2 style="width: 350px;height: 430px;color:whitesmoke; font-family:cursive;font-size: 22px">
                   <img src="Photo/point.jpg" width="350px" height="430px">
                   
                    </h2></div>
                    <div id="right">
                    <h1>
                    <form action="show.jsp">
                        <center> 
            <table>
                <tr><br>
                    <td><br><br>
                        <h1 style="font-size: 22px;font-family: cursive; color:#00dd22;"> Enter your registration number </h1>
                    </td>
            </tr>
            <td><br>
                    <tr><br>
                        <input type="number" name="r">
                    </tr>
                    </td>
                <tr><br>
                <td><br><br><br>
                    <center>
                        <input type="submit" value="Click here to get your ICard" style="width: 400px;height: 50px;font-size: 30px">
                    </center>
                    </td>
                </tr>
            </table>
                        </center>
        </form>
                
                
                       
                
                
                    
                </div>
            </div>
            
        </div>
    </body>
</html>

 <div id="header">
     
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="Photo/logo1_1.png">
     <h1 style="text-align: center; padding-top: 20px; font-size:40pt; color:gold; font-family: BookMan Old Style"></h1>
        </div>
        
        <html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>
    
    <body>
       <jsp:includepage="header.jsp"/>
        <div id="body">
            <jsp:includepage="Menu.jsp"/>
                

            <div id="content">
                
                
                <center>
                    <br>
                    <h1 style="color:#00dd22; font-family: Annabel Script; font-size:30pt;"><i>Online OPD <br> Registration Made Easy <br> Contact with patients moves..</i> </h1>
                    <marquee width=1100 height=400>
                        <img src="Photo/8.jpg" width="700">
                        <img src="Photo/6.jpg" width="700">
                        <img src="Photo/9.jpg" width="700">
                        <img src="Photo/7.jpg" width="700">
                    </marquee>
                   
                    </center>
            </div>
        </div>
    </body>
</html>

<html>
    <head>
        <title>testing....</title>
        <link href="style.css" rel="stylesheet">
    </head>
    <body>
        <jsp:includepage="header.jsp"/>
        
       
              
                 
                  
            </div>
            <div id="body">
                 <jsp:includepage="Menu.jsp"/>
                <div id="content">
                
                
                <center>
                    <br>
                    <h1 style="color:#00dd22; font-family: Annabel Script; font-size:25pt;"><i>Registration for ICard </i> </h1>
                  
                    <div id="left">
                       
                    <h2 style="width: 270px;height: 500px;color:whitesmoke; font-family:cursive;font-size: 22px">
                    Welcome  to the online ICard registration.
                    This registration is free of cost and each and every patient must get registered in this portal before the treatment session starts.
                    Every user must fill all the details required or mentioned in the portal.please submit or upload your photograph.
                    </h2></div>
                    <div id="right">
                    <h1>
                    
                       <a href="reg.jsp" >Click here to register for ICards</a><br><br>
                    
                    
                            <img src="Photo/line.jpg" width="350px" height="270px" margin-top="10px"><br><br>
                        
                    
                    
                   
                    <a href="fill.jsp">Click here to get your ICard</a>
                    </h1>
                    </div>    
                    
                    
                </centre>
                
            </div>
            
        </div>
    </body>
</html>
<center>
                                
            <html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br><br>

                        <center>

                            <form action="LoginCheck" method="post">
                                <center>
                                    <table>  

                                        <center>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src='Photo/123.png'><br>
                                            <br></center>
                                        <tr>
                                            <td>
                                        <z style='font-family: cursive; color: #00dd22; font-weight: bold'>  Username</z>
                                        </td>
                                        <td>
                                            <input type='text' name="u" required></td>
                                        </tr>

                                        <tr>

                                            <td>
                                        <z style='font-family: cursive; color:#00dd22;font-weight: bold'> Password </z>
                                        </td>
                                        <td><input type='password' name="p" required>
                                        </td>
                                        </tr>

                                    </table>
                                    <br>
                                    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<input type='image' src='Photo/login-icon1.png'>   
                                </center>
                                <p style="font-family: cursive; font-size: 15pt; color: red">Invalid User Id or Password </p>

                            </form>
                        </center>
                    </div>
                </div>
            </body>
        </html>
        
        <html>
    <head>
        <link href="style.css" rel="stylesheet">

        <script>


            function isNumber(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if (charCode > 31 && (charCode < 48 || charCode > 57)) {
                    return false;
                }
                return true;
            }




            function ValidateAlpha(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode < 65 || charCode > 90) && (charCode < 97 || charCode > 123) && charCode !== 32) {
                    return false;
                }
                return true;
            }

        </script>

    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br><br>

                        <center>
                            <h1 style="color:#00dd22; font-family: cursive; font-size:24pt;"><u> Check Patient Status</u></h1><br>
                            <form action="Status.jsp" method="post">
                                <table style="color:yellow; font-weight: bold; font-size:14pt">
                                    <tr>
                                        <td>Registration No                     </td>
                                        <td><input type="text" name="r" required placeholder="Enter Registration No" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Name                    </td>
                                        <td><input type="text" name="n" required placeholder="Enter Registered Name" onkeypress="return ValidateAlpha(event)"></td>

                                    </tr>

                                </table>
                                <br>
                                <input type="image" src="Photo/submit1.png">
                            </form>
                            <p style="font-family: cursive; font-size:16pt;color:Red">Registration No & name does not match. <br> Kindly Enter the registered name here.</p>
                        </center>
                    </div>
                </div>
            </body>
        </html>
        
        <%
    if(session.getAttribute("uid")==null)
{
response.sendRedirect("Invalid.jsp");
}
else if(session.getAttribute("usertype").toString().equals("Doctor"))
{
response.sendRedirect("Doctor.jsp");
}

else if(session.getAttribute("usertype").toString().equals("Clerk"))
{
response.sendRedirect("Reception.jsp");
}
 else if(session.getAttribute("usertype").toString().equals("Patient"))
{
response.sendRedirect("Patient.jsp");
}   
%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <div id="left">
                        
                        <br><br>

                        <center>
                            <marquee width=300 height=500 direction="up">
                        <img src="Photo/doct.jpg">
                        <img src="Photo/34.jpg">
                        <img src="Photo/l.jpg">
                        <img src="Photo/us.png">
                        <img src="Photo/li.jpg">
                            </marquee>
                        </center>
                    </div>
                        <div id="right">
                            <center>
                               
                        <br><br>

                        <center>

                            <form action="LoginCheck" method="post">
                                <center>
                                
                                    <table>  

                                        <center>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src='Photo/123.png'><br>
                                            <br></center>
                                        <tr>
                                            <td>
                                        <z style='font-family: cursive; color: #00dd22; font-weight: bold'>  Username</z>
                                        </td>
                                        <td>
                                            <input type='text' name="u" required placeholder="Enter Your User ID"></td>
                                        </tr>

                                        <tr>

                                            <td>
                                        <z style='font-family: cursive; color:#00dd22;font-weight: bold'> Password </z>
                                        </td>
                                        <td><br><input type='password' name="p" required placeholder="Enter password">
                                        </td>
                                        </tr>

                                    </table>
                                    <br>
                                    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<input type='image' src='Photo/login-icon1.png'>   
                                </center>

                            </form>
                        </center>
                    </div>
                </div>
            </body>
        </html>
        
        <%session.invalidate();%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>
    
    <body>
       <jsp:includepage="header.jsp"/>
        <div id="body">
            <jsp:includepage="Menu.jsp"/>
                

            <div id="content">
                <br><br>
                
                <center>
                    <img src="Photo/4.jpg" width="1100" height="480">
                
                    </center>
            </div>
        </div>
    </body>
</html>

<% if ((session.getAttribute("uid") == null) && (session.getAttribute("usertype") == null)) { %>
<div id="menu">
    <a href="AboutUS.jsp"> About Us </a> <br>
    <a href="Features.jsp"> Features </a> <br>
    <a href="CheckStatus.jsp"> Know Status </a> <br>
    <% if ((session.getAttribute("uid") == null)) { %>
    <a href="LoginPage.jsp"> Login Here  </a> <br>
    <% } else { %>
    <a href="Logout.jsp"> Logout </a> <% } %>
    <a href="ContactUs.jsp"> Contact Us </a>
</div>
<% } %>

<% if ((session.getAttribute("uid") != null) && (session.getAttribute("usertype") != null)) { %>

<% if (session.getAttribute("usertype").toString().equals("Clerk")) { %>
<div id="menu">
    <a href="Register.jsp"> Register Here </a> <br>
    <a href="Update.jsp"> Update Here  </a> <br>
    <a href="PatientsQueue.jsp">Queue</a>
    <a href="CheckStatus.jsp"> Check Status </a>
    <a href="Report.jsp"> Report </a>

    <a href="index1.jsp"> Generate ICard </a>
    <a href="Logout.jsp">Logout </a>
</div>
<% } %>

<% if ((session.getAttribute("usertype")).toString().equals("Patient")) { %>
<div id="menu">
    <a href="index.jsp"> Home </a> <br>
    <a href="AboutUS.jsp"> About Us </a> <br>
    <a href="CheckStatus.jsp"> Check Status </a>
    <a href="ContactUs.jsp"> Contact Us </a>

    <a href="Logout.jsp">Logout </a>
</div>
<% } %>

<% if ((session.getAttribute("usertype")).toString().equals("Doctor")) { %>
<div id="menu">
    <a href="Patients.jsp">Queue</a>
    <a href="Closed.jsp"> Closed Cases</a>
    <a href="p2_1.jsp"> View Reports</a>
    <a href="Pres.jsp"> Prescription</a>
    <a href="Logout.jsp">Logout </a>
</div>
<% } %>
<% }%>

<html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <div id="left">

                            <form action="a.jsp">

                                <center>
                                    <table>
                                        <tr><br><br>
                                        <td>
                                            <h2 style="color:#00dd22">Registration number:</h2  >
                                        </td>
                                        <td>
                                            <input type="number" name="r" >
                                        </td>
                                        </tr>
                                        <tr>
                                            <td>
                                                <h2 style="color:#00dd22">Patient Name:</h2>
                                            </td>
                                            <td>
                                                <input type="text" name="n">
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>
                                                <h2 style="color:#00dd22">Doctor:</h2>
                                            </td>
                                            <td>
                                               <Select name="c" required>
                                                <option> Dr. Kumar </option>
                                                <option> Dr. Agarwal</option>
                                                <option> Dr. Singh </option>
                                            </Select>
                                            </td>
                                        </tr>

                                        <tr>
                                            <td>
                                                <h2 style="color:#00dd22"> Prescription</h2>

                                            </td>
                                            <td>
                                                <textarea cols="30" rows="10" name="bg"></textarea>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td><br><br><br>
                                        <center>
                                            <input type="submit" value="Click to register" style="width: 200px;height: 40px"> 
                                        </center>
                                        </td>
                                        </tr>
                                    </table>
                                    <% if (request.getParameter("err") != null) {%>
                                    <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22">Unable to submit</p>
                                    <%

                                        }
                                        if (request.getParameter("a") != null) {%>
                                    <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22">Successfully Submitted</p>
                                    <%
                                        }

                                    %>

                                </center>
                            </form>



                        </div>
                        <div id="right">

                        </div>
                    </div>
                </div>
            </body>
        </html>
        
        <html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <div id="left">

                            <form action="s.jsp">
                                <center> 
                                    <table>
                                        <tr><br>
                                        <td><br><br>
                                            <h1 style="font-size: 25px;font-family: sans-serif;color:#00dd22"> Enter your Registration Number: </h1>
                                        </td>
                                        <td><br><br><br>
                                            <input type="number" name="r">
                                        </td>
                                        </tr>
                                        <tr><br>
                                        <td><br><br><br>
                                        <center>
                                            <input type="submit" value="Click here to view your records" style="width: 300px;height: 50px;font-size:18px">
                                        </center>
                                        </td>
                                        </tr>
                                    </table>
                           
                                </center>
                            </form>

                        </div>
                        <div id="right">

                        </div>
                    </div>
                </div>
            </body>
        </html>
        
        <html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <div id="left">

                            <form action="ViewReport.jsp">
                                <center> 
                                    <table>
                                        <tr><br>
                                        <td><br><br>
                                            <h1 style="font-size: 25px;font-family: sans-serif;color:#00dd22"> Enter your Registration Number: </h1>
                                        </td>
                                        <td><br><br><br>
                                            <input type="number" name="r">
                                        </td>
                                        </tr>
                                        <tr><br>
                                        <td><br><br><br>
                                        <center>
                                            <input type="submit" value="Click here to view your records" style="width: 300px;height: 50px;font-size:18px">
                                        </center>
                                        </td>
                                        </tr>
                                    </table>
                           
                                </center>
                            </form>

                        </div>
                        <div id="right">

                        </div>
                    </div>
                </div>
            </body>
        </html>
        
        <% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Patient"))){ %>
    
    
<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>
    
    <body>
       <jsp:includepage="header.jsp"/>
        <div id="body">
            <jsp:includepage="Menu.jsp"/>
                

            <div id="content">
                <br><br>
                
                <center>
                    <h1 style="color:#00dd22; font-family: cursive; font-size:34pt;"> Welcome to Patient Portal</h1><br>
                    <marquee width=1100 height=1000>
                        <img src="Photo/reception.png">
                        <img src="Photo/r2.jpg">
                        <img src="Photo/r3.jpg">
                    </marquee>
                    </center>
            </div>
        </div>
    </body>
</html>
<% } 

%>

<% if ((session.getAttribute("uid") == null) && (session.getAttribute("usertype") == null)) {
         response.sendRedirect("Invalid.jsp");
     }
     if ((session.getAttribute("uid") != null) && (session.getAttribute("usertype").toString().equals("Doctor"))) { %>


<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br>

                        <center>
                            <%
                                String doc = (String) session.getAttribute("uid");
                                Class.forName("oracle.jdbc.OracleDriver");
                                Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

                                PreparedStatement ps1 = cn.prepareStatement("select regno, name, age, status from patient where Doc=? AND STATUS='Open' order by regno");

                                ps1.setString(1, doc);
                                ResultSet rs = ps1.executeQuery();


                            %>

                            <center><p style='color:red;font-family: cursive; font-size:20pt;'><u>OPD Queue </u></p></center>

                            <center>
                                <form action="Close.jsp">
                                    <table style="border:5px solid cyan">

                                        <tr>
                                            <td width="120px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Reg No </p></center></td>
                                        <td width="200px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Name </p></center></td>
                                        <td width="50px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Age </p></center></td>
                                        <td width="100px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Status </p></center></td>
                                        <td width="40px;"><center> <p style="font-family: cursive;font-weight: bold; font-size:16pt; color:yellow"> Close </p></center></td>
                                        </tr>
                                        <%      while (rs.next()) {
                                                String regno = rs.getString(1);
                                                String name = rs.getString(2);
                                                String age = rs.getString(3);
                                                String status = rs.getString(4);%>
                                        <tr>
                                            <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=regno%> </p></center></td>
                                        <td width="100px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=name%> </p></center></td>
                                        <td width="50px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=age%> </p></center></td>
                                        <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=status%> </p></center></td>

                                        <td width="30px;"><center><p style="font-family: cursive;font-weight: bold; color:#00dd22"> <input type="radio" value="<%=regno%>" name="v" required="required"></p></td>

                                            </tr>






                                <% if ((session.getAttribute("uid") == null) && (session.getAttribute("usertype") == null)) {
        response.sendRedirect("Invalid.jsp");
    }
    if ((session.getAttribute("uid") != null) && (session.getAttribute("usertype").toString().equals("Clerk"))) { %>


<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br>
                        <center><p style='color:red;font-family: cursive; font-size:20pt;'><u>OPD Queue </u></p></center>

                        <center>

                            <table style="border:5px solid cyan">

                                <tr>
                                    <td width="120px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Reg No </p></center></td>
                                <td width="200px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Name </p></center></td>
                                <td width="50px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Age </p></center></td>
                                <td width="100px;"><center> <p style="font-family: cursive;font-size:16pt;font-weight: bold; color:yellow"> Status </p></center></td>
                                <td width="120px;"><center> <p style="font-family: cursive;font-weight: bold; font-size:16pt; color:yellow"> Doctor </p></center></td>
                                <td width="40px;"><center> <p style="font-family: cursive;font-weight: bold; font-size:16pt; color:yellow"> Inform </p></center></td>

                                </tr>

                                <center>
                                    <%
                                        Class.forName("oracle.jdbc.OracleDriver");
                                        Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

                                        PreparedStatement ps1 = cn.prepareStatement("select regno, name, age, status,doc,mobile,rownum from patient where Doc=? AND STATUS='Open' and rownum<=2 order by regno");

                                        ps1.setString(1, "Dr. Kumar");
                                        ResultSet rs = ps1.executeQuery();

                                        while (rs.next()) {
                                            String regno = rs.getString(1);
                                            String name = rs.getString(2);
                                            String age = rs.getString(3);
                                            String status = rs.getString(4);
                                            String doc = rs.getString(5);
                                            String mobile = rs.getString(6);
                                            String rownum = rs.getString(7);
                                    %>
                                    <tr>
                                        <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=regno%> </p></center></td>
                                    <td width="100px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=name%> </p></center></td>
                                    <td width="50px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=age%> </p></center></td>
                                    <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=status%> </p></center></td>
                                    <td width="120px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=doc%> </p></center></td>
                                    <td width="120px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"><a href="sendsms.jsp?rownum=<%=rownum%>&mobile=<%=mobile%>&name=<%=name%>&doc=<%=doc%>"><button>Send SMS</button></a></p></center></td>


                                    </tr>






                                    <%} %>


                                    <%
                                        PreparedStatement ps2 = cn.prepareStatement("select regno, name, age, status,doc,mobile,rownum from patient where Doc=? AND STATUS='Open' and rownum<=2 order by regno");

                                        ps2.setString(1, "Dr. Singh");
                                        ResultSet rs1 = ps2.executeQuery();

                                        while (rs1.next()) {
                                            String regno = rs1.getString(1);
                                            String name = rs1.getString(2);
                                            String age = rs1.getString(3);
                                            String status = rs1.getString(4);
                                            String doc = rs1.getString(5);
                                            String mobile = rs1.getString(6);
                                            String rownum = rs1.getString(7);
                                    %>
                                    <tr>
                                        <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=regno%> </p></center></td>
                                    <td width="100px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=name%> </p></center></td>
                                    <td width="50px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=age%> </p></center></td>
                                    <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=status%> </p></center></td>
                                    <td width="120px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=doc%> </p></center></td>
                                    <td width="120px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"><a href="sendsms.jsp?rownum=<%=rownum%>&mobile=<%=mobile%>&name=<%=name%>&doc=<%=doc%>"><button>Send SMS</button></a></p></center></td>


                                    </tr>






                                    <%} %>
                                    <%  PreparedStatement ps3 = cn.prepareStatement("select regno, name, age, status,doc,mobile,rownum from patient where Doc=? AND STATUS='Open' and rownum<=2 order by regno");

                                        ps3.setString(1, "Dr. Agarwal");
                                        ResultSet rs3 = ps3.executeQuery();

                                        while (rs3.next()) {
                                            String regno = rs3.getString(1);
                                            String name = rs3.getString(2);
                                            String age = rs3.getString(3);
                                            String status = rs3.getString(4);
                                            String doc = rs3.getString(5);
                                            String mobile = rs3.getString(6);
                                            String rownum = rs3.getString(7);
                                    %>
                                    <tr>
                                        <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=regno%> </p></center></td>
                                    <td width="100px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=name%> </p></center></td>
                                    <td width="50px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=age%> </p></center></td>
                                    <td width="80px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=status%> </p></center></td>
                                    <td width="120px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"> <%=doc%> </p></center></td>
                                    <td width="120px;"><center> <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22"><a href="sendsms.jsp?rownum=<%=rownum%>&mobile=<%=mobile%>&name=<%=name%>&doc=<%=doc%>"><button>Send SMS</button></a></p></center></td>


                                    </tr>






                                    <%} %>

                            </table>

                            <br>
                            <% if (request.getParameter("err") != null) {%>
                            <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22">Unable to send SMS</p>
                            <%

                                }
                                if (request.getParameter("s") != null) {%>
                            <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22">SMS sent</p>
                            <%
                                }

                            %>





                        </center>

                    </div>

                </div>
                <%                    cn.close();
                %>
            </body>
        </html>
        <% }%>

<html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>

                    <div id="content">
                        <div id="left">
                            <center>
                                <br>
                                <a href="p.jsp" style="align:right;font-size: 20pt; color: white"> Click here to enter new record</a>
                            <br><br><br>
                            <a href="p2.jsp" style="align:right;font-size: 20pt; color: white"> Click here to see previous records </a>  
                            </center>
                            
                            <marquee width=1100 height=500 direction="left">
                            <img src="Photo/p.jpg">
                            <img src="Photo/p2.jpg">
                            <img src="Photo/p1.jpg">
                            <img src="Photo/p3.jpg">
                            <img src="Photo/p4.jpg">
                            <img src="Photo/p5.jpg">
                            </marquee>
                           
                            
                    </div>
                        <div id="right">
                            
                        </div>
                    </div>
                </div>
            </body>
        </html>
        
        <% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Clerk"))){ %>
    
    
<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>
    
    <body>
       <jsp:includepage="header.jsp"/>
        <div id="body">
            <jsp:includepage="Menu.jsp"/>
                

            <div id="content">
                <br><br>
                
                <center>
                    <h1 style="color:#00dd22; font-family: cursive; font-size:34pt;"> Welcome to OPD Reception Portal</h1><br>
                    <marquee width=1100 height=1000>
                        <img src="Photo/reception.png">
                        <img src="Photo/r2.jpg">
                        <img src="Photo/r3.jpg">
                    </marquee>
                    </center>
            </div>
        </div>
    </body>
</html>
<% } 

%>

<html>
    <head>
        <title>testing....</title>
        <link href="style.css" rel="stylesheet">
    </head>
    <body>
        <jsp:includepage="header.jsp"/>
        
        
                  
      
            <div id="body">
                 <jsp:includepage="Menu.jsp"/>
                <div id="content">
      
                
                <center>
                    <br>
                    <h1 style="color:#00dd22; font-family: Annabel Script; font-size:25pt;"><i>Registration for ICard </i> </h1>
                  
                    <div id="left">
                       <img src="Photo/reg.jpg" width="200px" height="430px">
                    </div>
                    <div id="right">
                    <h1>
                      <form action="add.jsp">
            
            <center>
                <table>
                    <tr>
                        <td>
                           <z style='font-family: cursive; color: #00dd22; font-size:13 ;'> 
                               <h1>Registration number</h1></z>
                        </td>
                        <td>
                            <input type="number" name="r">
                        </td>
                    </tr>
                    <tr>
                        <td>
                              <z style='font-family: cursive; color: #00dd22; font-size:13 ;'> 
                                  <h1>Patient Name</h1></z>
                        </td>
                        <td>  <z style='font-family: cursive; color: #00dd22; font-size:13 ;'> 
                            
                            <input type="text" name="n"></z>
                        </td>
                    </tr>
                    <tr>
                        <td>  <z style='font-family: cursive; color: #00dd22; font-size:13 ;'> 
                        <h1>Age</h1></z>
                        </td>
                        <td>
                             <input type="text" name="a">
                        </td>
                    </tr>
                    <tr>
                        <td>  <z style='font-family: cursive; color: #00dd22 ;font-size:13 ; '> 
                        <h1>Diagnosed with</h1></z>
                        </td>
                        <td>
                             <input type="text" name="dia">
                        </td>
                    </tr>
                    
                    <tr>
                        <td>  <z style='font-family: cursive; color: #00dd22; font-size:13 ;'> 
                            <h1> Doctor</h1>
                    </z>
                        </td>
                        <td>
                             <input type="text" name="d">
                        </td>
                    </tr>
                    <tr>
                        <td><z style='font-family: cursive; color: #00dd22; font-size:13 ;'> <h1>Mobile Number</h1></z>    </td>
                         <td><input type="text" name="m" required maxlength="10" placeholder="Enter 10 digits mobile no" onkeypress="return isNumber(event)"></td>

                                    </tr>
                    
                   
                    <tr>
                        <td>
                            <input type="submit" value="Click to register" style="width: 200px; height: 40px"> 
                        </td>
                    </tr>
                </table>
                    
            </center>
        </form>
  
                
                   
                </div>
            </div>
            
        </div>
    </body>
</html>

       
                      <% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Clerk"))){ %>
 
<html>
    <head>
        <link href="style.css" rel="stylesheet">
        <script>


            function isNumber(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if (charCode > 31 && (charCode < 48 || charCode > 57)) {
                    return false;
                }
                return true;
            }




            function ValidateAlpha(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode < 65 || charCode > 90) && (charCode < 97 || charCode > 123) && charCode !== 32) {
                    return false;
                }
                return true;
            }

        </script>


    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br><br>

                        <center>
                            <h1 style="color:#00dd22; font-family: cursive; font-size:24pt;"><u> Registration</u></h1><br>
                            <form action="SaveRegister.jsp">
                                <table style="color:yellow; font-weight: bold; font-size:14pt">
                                    <tr>
                                        <td>Name                     </td>
                                        <td><input type="text" name="n" required placeholder="Enter Name" onkeypress="return ValidateAlpha(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Age                         </td>
                                        <td><input type="number" name="a" required min="1" max="120" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Diagnosis                         </td>
                                        <td><input type="text" name="d" required placeholder="You are Diagnosed With?"></td>

                                    </tr>
                                    <tr>
                                        <td>Doctor                         </td>
                                        <td><Select name="doc" required>
                                                <option> Dr. Kumar </option>
                                                <option> Dr. Agarwal</option>
                                                <option> Dr. Singh </option>
                                            </Select> </td>

                                    </tr>
                                    <tr>
                                        <td>Mobile                         </td>
                                        <td><input type="text" name="m" required maxlength="12" placeholder="919xxxxxxxxx" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Fee                         </td>
                                        <td><input type="text" name="f" required placeholder="Enter Fee Deposited" onkeypress="return isNumber(event)"></td>

                                    </tr>



                                </table>
                                <br>
                                <input type="image" src="Photo/submit1.png">
                            </form>
                        </center>
                    </div>
                </div>
            </body>
        </html>
        
        <% }


        %>
        
        <html>
    <head>
        <link href="style.css" rel="stylesheet">



    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <div id="left">

                            <form action="savereport.jsp">

                                <center>
                                    <table>
                                        <tr><br><br>
                                        <td>
                                            <h2 style="color:#00dd22">Registration number:</h2>
                                        </td>
                                        <td>
                                            <input type="number" name="r" >
                                        </td>
                                        </tr>
                                      
                                        <tr>
                                            <td>
                                                <h2 style="color:#00dd22">Doctor:</h2>
                                            </td>
                                            <td>
                                               <Select name="c" required>
                                                <option> Dr. Kumar </option>
                                                <option> Dr. Agarwal</option>
                                                <option> Dr. Singh </option>
                                            </Select>
                                            </td>
                                        </tr>

                                        <tr>
                                            <td>
                                                <h2 style="color:#00dd22"> Report</h2>

                                            </td>
                                            <td>
                                                <textarea cols="30" rows="10" name="bg"></textarea>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td><br><br><br>
                                        <center>
                                            <input type="submit" value="Submit" style="width: 100px;height: 40px"> 
                                        </center>
                                        </td>
                                        </tr>
                                    </table>
                                    <% if (request.getParameter("err") != null) {%>
                                    <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22">Unable to submit</p>
                                    <%

                                        }
                                        if (request.getParameter("a") != null) {%>
                                    <p style="font-family: cursive;font-size:14pt;font-weight: bold; color:#00dd22">Successfully Submitted</p>
                                    <%
                                        }

                                    %>

                                </center>
                            </form>



                        </div>
                        <div id="right">

                        </div>
                    </div>
                </div>
            </body>
        </html>
        
        <%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.Connection"%>
<%@page import="java.sql.PreparedStatement"%>
<html>

    <head>
        <title>testing....</title>
        <link href="style.css" rel="stylesheet">
        <style>
            td{
                color:white;
                font-weight: bold;
            }
            tr{
                color:yellow;
            }
        </style>
    </head>
    <body>
        <jsp:includepage="header.jsp"/>

        </div>
        <div id="body">

            <jsp:includepage="Menu.jsp"/>



                <center>
                    
                    <%
                        int r = Integer.parseInt(request.getParameter("r"));
                        Class.forName("oracle.jdbc.OracleDriver");
                        Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

                        PreparedStatement ps = cn.prepareStatement("select * from pres where regnumber=?");
                        ps.setInt(1, r);

                        ResultSet rs = ps.executeQuery();
                        while (rs.next()) {

                            String n = rs.getString(2);

                            String c = rs.getString(3);
                            String bg = rs.getString(4);

                    %>
                    <div id="content">
                        <br><br>
                        <table width="400px" border="2">
                            <tr>
                                <td colspan="2" style="color:yellow; font-weight: bold; font-size:14pt"><center>Patient Prescription</center></td>

                            </tr>
                            <tr>
                                <td>
                                    Registration no.
                                </td>
                                <td>
                                    <%=r%>
                                </td>



                            </tr>
                            <tr>
                                <td>
                                    Patient name
                                </td>
                                <td>
                                    <%=n%>
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    Doctor
                                </td>
                                <td>
                                    <%=c%>
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    Prescription
                                </td>
                                <td>
                                    <%=bg%>
                                </td>
                            </tr>

                        </table>
                        <%
                            }
                            cn.close();
                            rs.close();
                            ps.close();
                        %>

                </center>
            </div>
        </body>
    </html>
    
    <% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Clerk"))){ %>

<%@page import="java.sql.ResultSet"%>

<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br><br>

                        <center>
                            <%

                                String n = request.getParameter("n");
                                String a = request.getParameter("a");
                                String d = request.getParameter("d");
                                String m = request.getParameter("m");
                                String f = request.getParameter("f");
                                String doc = request.getParameter("doc");
                                Class.forName("oracle.jdbc.OracleDriver");
                                Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

                                PreparedStatement ps1 = cn.prepareStatement("select count(*) from patient");
                                ResultSet rs = ps1.executeQuery();
                                rs.next();
                                int count = Integer.parseInt(rs.getString(1))+1;
                                String regno = "100" + count;
                                PreparedStatement ps = cn.prepareStatement("insert into patient(regno,name,age,diagnosis,mobile,fee,doc) values(?,?,?,?,?,?,?)");

                                ps.setString(1, regno);
                                ps.setString(2, n);
                                ps.setInt(3, Integer.parseInt(a));
                                ps.setString(4, d);
                                ps.setString(5, m);
                                ps.setInt(6, Integer.parseInt(f));
                                ps.setString(7, doc);
                            %>
                            <br>
                            <br>
                            <br>

                            <b style='color:#00dd22; font-family:cursive; font-size: 25px;'> Registered Successfully. <br> Your Registration No is: <%=regno%> </b>

                            <%
                                ps.executeUpdate();
                                cn.close();
                            %>

                        </center>
                    </div>
                </div>
            </body>
        </html>


        <%}
       
        %>
        
        <<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.Connection"%>
<html>
    <body>
        <%
            try {
                String r = request.getParameter("r");
                String c = request.getParameter("c");

                String bg = request.getParameter("bg");
                Class.forName("oracle.jdbc.OracleDriver");
                Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");
                PreparedStatement ps = cn.prepareStatement("insert into report values(?,?,?)");
                ps.setString(1, r);
                ps.setString(2, c);
                ps.setString(3, bg);

//            out.println("<b style='color:#00dd22; font-family:cursive; font-size: 65px;' Registered Successfully </b>");

                ps.executeUpdate();
                response.sendRedirect("Report.jsp?a=abc");
                ps.close();
                cn.close();

            } catch (Exception e) {
                response.sendRedirect("Report.jsp?err=abc");

            }
        %>
    </body>
</html>

<%@page import="OPD.SmsLane"%>
<%
    try {
        int rownum = Integer.parseInt(request.getParameter("rownum"));
        String name = request.getParameter("name");
        String doc = request.getParameter("doc");

        String mobile = request.getParameter("mobile");
        SmsLane sms=new SmsLane();
        String msg = "";
        if (rownum == 1) {
            msg = "Dear "+name+", Your appointment with "+doc+" is in 30 mins. Please reach on time. -The OPD Team";
        }
        if (rownum == 2) {
            msg = "Dear "+name+", Your appointment with "+doc+" is in 60 mins. Please reach on time. -The OPD Team";
        }

        sms.SMSSender(mobile, msg);
        response.sendRedirect("PatientsQueue.jsp?s=success");
    } catch (Exception e) {
        response.sendRedirect("PatientsQueue.jsp?err=success");

    }
%>


<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.Connection"%>
<%@page import="java.sql.PreparedStatement"%>
<html>
   
    <head>
        <title>testing....</title>
        <link href="style.css" rel="stylesheet">
    </head>
    <body>
        <jsp:includepage="header.jsp"/>
                  
            </div>
            <div id="body">
                
                 <jsp:includepage="Menu.jsp"/>
                     
                
                
                <center>
<%
    int r = Integer.parseInt(request.getParameter("r"));
    Class.forName("oracle.jdbc.OracleDriver");
    Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");
   
    PreparedStatement ps = cn.prepareStatement("Select * from icard where regno=?");
    ps.setInt(1, r);

    ResultSet rs = ps.executeQuery();
    while (rs.next()) {

        String n = rs.getString(2);
        int a = rs.getInt(3);
        String dia = rs.getString(4);
        String d = rs.getString(5);
        String m = rs.getString(6); 
%>

        <table width="400px" border="1">
            <tr>
                <td colspan="3" style="color:red"><center>Patient ICard</center></td>
            
        </tr>
        <tr>
            <td>
                Registration no.
            </td>
            <td>
               <%=r%>
            </td>
            
            
                <td row span="6"><img src="Photo/MI7.jpg">
            </td>
        </tr>
        <tr>
            <td>
                Patient name
            </td>
            <td>
                <%=n%>
            </td>
        </tr>
        <tr>
            <td>
                Age
            </td>
            <td>
                <%=a%>
            </td>
        </tr>
        <tr>
            <td>
                Diagnosed with
            </td>
            <td>
               <%=dia%>
            </td>
        </tr>
        <tr>
            <td>
                Doctor
            </td>
            <td>
                <%=d%>
            </td>
        </tr>
        <tr>
            <td>
                Mobile no.
            </td>
            <td>
                <%=m%>
            </td>
        </tr>
    </table>
                <%
                  }
    cn.close();
    rs.close();
    ps.close();
    %>
    <br><br><br>
    <input type="image" src="Photo/print.jpg" onclick="javascript:window.print()" >
                </center>
</body>
</html>

<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>


<%
    String r = request.getParameter("r");
    String n = request.getParameter("n");
    Class.forName("oracle.jdbc.OracleDriver");
    Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

    PreparedStatement ps1 = cn.prepareStatement("select name from patient where regno=?");

    ps1.setString(1, r);
    ResultSet rs = ps1.executeQuery();
    if (rs.next()) {
        String name = rs.getString(1);
        if (n.equals(name)) {
            response.sendRedirect("CurrentStatus.jsp");
            session.setAttribute("PatientReg", r);
        } else {
            response.sendRedirect("InvalidCredentials.jsp");
        }
    }
    else
    {
        response.sendRedirect("CheckStatus.jsp?err=y");
    }

    cn.close();
%>

#body{
    height:545px;
    width:100%;
}

#content
{

    height:545px;
    width:84.9%;
    background-color:#E9E4C7;
    background-image:url(Photo/pattern.png);
    float:left;
}
#right
{
    height:545px;
    width:45%;

    float:left;

}
#left
{
    height:545px;
    width:55%;

    float:left;

}
#header
{

    height:120px;
    width:100%;
    background-image:url(Photo/head_1.png);
}
#menu
{


}

#menu
{
    height:545px;
    width:200px;
    float:left;
    background-image:url(Photo/bg3.jpg);
}
#menu a{
    text-decoration: none;
    display: block;
    width:180px;
    padding-bottom: 20px;
    padding-top: 20px;
    padding-left:30px;
    padding-right: 30px;
    margin-bottom: 1px;
    color:white;
    font-weight: bold;
    font-family: cursive;
    float:left;
    font-size:16pt;
} 
#menu a:hover
{
    color: #00dd22;
    background-color:black;
    font-weight: bolder;
    font-family:cursive;
}
a
{
   
    color:black;
    
   
    font-size:28px;
    font-family: cursive;
}
a:hover
{
    
    color:red;
}


#b
{
    width:1000px;
    height:500px;
    background-color: red;
}

#w
{
    width:1000px;
    height:600px;
    border-width: thick;
    border-style: groove;
}
#h
{
    width:1000px;
    height:100px;
    background-color: pink;
    font-size: 80px;
    text-decoration: blink;
    color: blue;
    border-style:outset;
 
   


}
a
{
   
    color:black;
    
   
    font-size:50px;
    font-family: cursive;
}
a:hover
{
    
    color:red;
}


#b
{
    width:1000px;
    height:500px;
    background-color: red;
}
#r
{
    width:800px;
    height:500px;
    background-color:bisque;
   
    float:right;
    font-size: 25;
}

#l
{
    width: 200px;
    height: 500px;
    background-color: blue;
    float:left;
}
#p
{
    width:800px;
    height:500px;
    background-color:bisque;
    background-image: url(index1.jpg);
   
    float:right;
    font-size: 25;
}
#m
{
    width:800px;
    height:500px;
    background-color:bisque;
    background-image: url(card.jpg);
   
    float:right;
    font-size: 25;
  
}

<% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Clerk"))){ %>
<html>
    <head>
        <link href="style.css" rel="stylesheet">
        <script>


            function isNumber(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if (charCode > 31 && (charCode < 48 || charCode > 57)) {
                    return false;
                }
                return true;
            }




            function ValidateAlpha(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode < 65 || charCode > 90) && (charCode < 97 || charCode > 123) && charCode !== 32) {
                    return false;
                }
                return true;
            }

        </script>


    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br><br>

                        <center>
                            <h1 style="color:#00dd22; font-family: cursive; font-size:24pt;"><u> Update Existing Record</u></h1><br>
                            <form action="UpdateRecord.jsp">
                                <table style="color:yellow; font-weight: bold; font-size:14pt">
                                    <tr>
                                        <td>Registration No:                    </td>
                                        <td><input type="number" name="r" required placeholder="Enter Registration No" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Name                     </td>
                                        <td><input type="text" name="n" required placeholder="Enter Name" onkeypress="return ValidateAlpha(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Age                         </td>
                                        <td><input type="number" name="a" required min="1" max="120" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Diagnosis                         </td>
                                        <td><input type="text" name="d" required placeholder="You are Diagnosed With?"></td>

                                    </tr>
                                     <tr>
                                        <td>Doctor                         </td>
                                        <td><Select name="doc" required>
                                                <option> Dr. Kumar </option>
                                                <option> Dr. Agarwal</option>
                                                <option> Dr. Singh </option>
                                            </Select> </td>

                                    </tr>
                                    <tr>
                                        <td>Mobile                         </td>
                                        <td><input type="text" name="m" required maxlength="10" placeholder="Enter 10 digits mobile no" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Fee                         </td>
                                        <td><input type="number" name="f" required placeholder="Enter Fee Deposited" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Status              </td>
                                        <td><Select name="s" required>
                                                <option>Open</option>
                                                <option>Close</option>
                                            </select>
                                        </td>

                                    </tr>


                                </table>
                                <br>
                                <input type="image" src="Photo/submit1.png">
                            </form>
                        </center>
                    </div>
                </div>
            </body>
        </html>
        <%}

         %>
         
         <% if((session.getAttribute("uid")==null) && (session.getAttribute("usertype")==null)){
    response.sendRedirect("Invalid.jsp");
}
    if((session.getAttribute("uid")!=null) && (session.getAttribute("usertype").toString().equals("Clerk"))){ %>
<html>
    <head>
        <link href="style.css" rel="stylesheet">
        <script>


            function isNumber(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if (charCode > 31 && (charCode < 48 || charCode > 57)) {
                    return false;
                }
                return true;
            }




            function ValidateAlpha(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode < 65 || charCode > 90) && (charCode < 97 || charCode > 123) && charCode !== 32) {
                    return false;
                }
                return true;
            }

        </script>


    </head>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br><br>

                        <center>
                            <h1 style="color:#00dd22; font-family: cursive; font-size:24pt;"><u> Update Existing Record</u></h1><br>
                            <form action="UpdateRecord.jsp">
                                <table style="color:yellow; font-weight: bold; font-size:14pt">
                                    <tr>
                                        <td>Registration No:                    </td>
                                        <td><input type="number" name="r" required placeholder="Enter Registration No" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Name                     </td>
                                        <td><input type="text" name="n" required placeholder="Enter Name" onkeypress="return ValidateAlpha(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Age                         </td>
                                        <td><input type="number" name="a" required min="1" max="120" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Diagnosis                         </td>
                                        <td><input type="text" name="d" required placeholder="You are Diagnosed With?"></td>

                                    </tr>
                                     <tr>
                                        <td>Doctor                         </td>
                                        <td><Select name="doc" required>
                                                <option> Dr. Kumar </option>
                                                <option> Dr. Agarwal</option>
                                                <option> Dr. Singh </option>
                                            </Select> </td>

                                    </tr>
                                    <tr>
                                        <td>Mobile                         </td>
                                        <td><input type="text" name="m" required maxlength="10" placeholder="Enter 10 digits mobile no" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Fee                         </td>
                                        <td><input type="number" name="f" required placeholder="Enter Fee Deposited" onkeypress="return isNumber(event)"></td>

                                    </tr>
                                    <tr>
                                        <td>Status              </td>
                                        <td><Select name="s" required>
                                                <option>Open</option>
                                                <option>Close</option>
                                            </select>
                                        </td>

                                    </tr>


                                </table>
                                <br>
                                <input type="image" src="Photo/submit1.png">
                            </form>
                        </center>
                    </div>
                </div>
            </body>
        </html>
        <%}

         %>
         
         <% if ((session.getAttribute("uid") == null) && (session.getAttribute("usertype") == null)) {
        response.sendRedirect("Invalid.jsp");
    }
    if ((session.getAttribute("uid") != null) && (session.getAttribute("usertype").toString().equals("Doctor"))) { %>


<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>

<html>
    <header>
        <link href="style.css" rel="stylesheet">
    </header>

    <body>
        <jsp:includepage="header.jsp"/>
            <div id="body">
                <jsp:includepage="Menu.jsp"/>


                    <div id="content">
                        <br>

                        <center>
                            <%
                                String doc = (String) session.getAttribute("uid");
                                String reg = request.getParameter("r");
                                Class.forName("oracle.jdbc.OracleDriver");
                                Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "opd", "opd");

                                PreparedStatement ps1 = cn.prepareStatement("select regno, report from report where Doc=? and regno=? order by regno");

                                ps1.setString(1, doc);
                                ps1.setString(2, reg);

                                ResultSet rs = ps1.executeQuery();


                            %>

                            <center><p style='color:red;font-family: cursive; font-size:20pt;'><u>OPD Queue </u></p></center>

                            <center>



