# Employee Management System CRUD Application

This is a group project developed for [Enterprises Architecture]. The project aims to develop a simple CRUD (Create, Read, Update, Delete) application for managing employee records. It is developed using Java with NetBeans as the IDE, Java Swing for the user interface, and MySQL for the database.

## Group Members

- KEG/IT/2021/F/0041 - Sandun LB
- KEG/IT/2021/F/0043 - Anjana
- KEG/IT/2021/F/0090 - Maduranga
- KEG/IT/2021/F/0120 - Sahan

## Features

- **Create:** Ability to add new employee records to the database.
- **Read:** View existing employee records.
- **Update:** Modify information of existing employee records.
- **Delete:** Remove employee records from the database.
- **GUI:** User-friendly graphical user interface built using Java Swing.
- **Database:** MySQL database backend for storing employee data.

## Tools Used

- **Java:** Programming language used for the application logic.
- **NetBeans:** Integrated Development Environment (IDE) for Java development.
- **Java Swing:** Toolkit for building graphical user interfaces in Java.
- **MySQL:** Relational database management system for storing employee data.

## Installation

1. Clone the repository to your local machine.
2. Import the project into NetBeans.
3. Set up the MySQL database with appropriate tables and configurations.
4. Configure the application to connect to your MySQL database.
5. Add all the necessary Java libraries.
6. Build and run the application.

## Usage

1. Launch the application.
2. Use the GUI to perform CRUD operations on employee records.
3. Explore various features such as searching and updating records.
4. Enjoy managing your employee data efficiently!

## Functionality by Group Members

In this application, it is divided into 2 main categories: **Add employees** and **Assign employees (assign Employees to the Job/Task**. Each category has its own CRUD operations. We had to create two interacting tables in the database because the assignment guide specifies that we must create at least two tables for CRUD Functions.

### Database Connection

```
public class Database {
    public static Connection connection(){
    
        
        try{
        
            Class.forName("com.mysql.jdbc.Driver");
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/Employee","root","");
            return con;
        
        }catch(Exception e){
            System.out.println(e);
            return null;
        }
        
    }

    static Connection getConnection() {
        throw new UnsupportedOperationException("Not supported yet."); // Generated from nbfs://nbhost/SystemFileSystem/Templates/Classes/Code/GeneratedMethodBody
    }
    
}
```

### Add Employees (Add Employee Details to Database)

- **>Create (Add Employee):** Implemented by **KEG/IT/2021/F/0041 - Sandun LB.**
- This functionality allows users to add new employee records to the database.


```
   Connection con = Database.connection();

        try{

            PreparedStatement ptst = con.prepareStatement("insert into employee (name,password,email,address,city,mobile) values(?,?,?,?,?,?)");
            ptst.setString(1, txtname.getText());
            ptst.setString(2, txtpassword.getText());
            ptst.setString(3, txtemail.getText());
            ptst.setString(4, txtaddress.getText());
            ptst.setString(5, txtcity.getText());
            ptst.setString(6, txtcontact.getText());

            int i = ptst.executeUpdate();

            if(i != 0){
                JOptionPane.showMessageDialog(null, "Employee Details Added Successfully !");
                clear();
            }

        } catch (SQLException e) {
            e.printStackTrace();
            JOptionPane.showMessageDialog(null, "You Must Fill all Fields to add the Database!!!");
        } catch (NumberFormatException e) {
            System.out.println("Invalid employee ID or salary format.");
        }
    }
```

  
  
- **>Read (View Employee):** Implemented by **KEG/IT/2021/F/0043 - Anjana.**
-  This functionality allows users to view existing employee records.

```
public void showData(){
Connection con = Database.connection();
        
        try{
        
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("select * from employee");
            
            
        DefaultTableModel model = (DefaultTableModel) view.getModel();
        model.setRowCount(0);
        
        while(rs.next()){
        
            String id = String.valueOf(rs.getString("id"));
            String name = rs.getString("name");
            String password = rs.getString("password");
            String email = rs.getString("email");
            String address = rs.getString("address");
            String city = rs.getString("city");
            String contact = rs.getString("contact");
            
            String addT [] = {id,name,password,email,address,city,contact};
            
            model.addRow(addT);
        
        }
        
        }catch(Exception e){
            System.out.println(e);
        }
    }
```

  
- **>Update (Update Employee):** Implemented by **KEG/IT/2021/F/0090 - Maduranga.**
-  This functionality allows users to modify information of existing employee records.


```
 Connection con = Database.connection();

        try{

            PreparedStatement ptst = con.prepareStatement("UPDATE employee SET name=?,password=?,email=?,address=?,city=?,contact=? WHERE id=?");
            ptst.setString(7, txtid.getText());
            ptst.setString(1, txtname.getText());
            ptst.setString(2, txtpassword.getText());
            ptst.setString(3, txtemail.getText());
            ptst.setString(4, txtaddress.getText());
            ptst.setString(5, txtcity.getText());
            ptst.setString(6, txtcontact.getText());

            int i = ptst.executeUpdate();

            if(i != 0){
                JOptionPane.showMessageDialog(null, "Employee Details Updated Successfully !");
                showData();
                clear();
            }

        } catch (SQLException e) {
            e.printStackTrace();
            JOptionPane.showMessageDialog(null, "You Must Fill all Fields to Update the Database!!!");
        } catch (NumberFormatException e) {
            System.out.println("Invalid employee ID or salary format.");
        }
    }
```               
  
- **>Delete (Delete Employee):** Implemented by **KEG/IT/2021/F/0120 - Sahan.**
-  This functionality allows users to remove employee records from the database.

  
```
 Connection con = Database.connection();

        try{

            Statement stmt = con.createStatement();
            int i = stmt.executeUpdate("delete from employee where id = '"+Integer.parseInt(txtid.getText())+"' ");

            if(i!= 0){
                JOptionPane.showMessageDialog(null, "Data Recoard Deleted Successfully!");
                txtid.setText("");
                showData();
            }

        }catch(Exception e){
            System.out.println(e);

        }
    }               
```


### Assign Employees (Assign Employees to Jobs/Task) 

- **>Create (Assign Employee):** Implemented by **KEG/IT/2021/F/0041 - Sandun LB.**
-  This functionality allows users to assign employees to specific tasks or jobs.

  
```
 Connection con = Database.connection();

        try{

            PreparedStatement ptst = con.prepareStatement("INSERT INTO employment_details (employee_id, department, job_title, employment_status, hire_date, salary) VALUES (?, ?, ?, ?, ?, ?)");


ptst.setInt(1, Integer.parseInt(txtemployeeid.getText()));
ptst.setString(2, txtdepartment.getText());
ptst.setString(3, txtjobtitle.getText());
ptst.setString(4, txtemploymentstatus.getText()); 
ptst.setString(5, txthiredate.getText()); 
double salary = Double.parseDouble(txtsalary.getText());
    ptst.setDouble(6, salary); 

// Execute the query
int i = ptst.executeUpdate();

            if(i != 0){
                JOptionPane.showMessageDialog(null, "Employee Details Added Successfully !");
                showData();
                clear();
            }
        

} catch (SQLException e) {
    e.printStackTrace(); // Handle SQL exception
} catch (NumberFormatException e) {
    System.out.println("Invalid employee ID or salary format.");
}
```
  
- **>Read (View Assigned Employee):** Implemented by **KEG/IT/2021/F/0043 - Anjana.**
-  This functionality allows users to view employees who are currently assigned to tasks or jobs.

  
```
  public void showData(){
Connection con = Database.connection();
        
        try {
    Statement stmt = con.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT * FROM employment_details");

    DefaultTableModel model = new DefaultTableModel(
        new Object[][]{
            {null, null, null, null, null, null}
        },
        new String[]{
            "Employee ID", "Department", "Job Title", "Employee Status", "Hire Date", "Salary"
        }
    );

    while (rs.next()) {
        int employeeId = rs.getInt("employee_id");
        String department = rs.getString("department");
        String jobTitle = rs.getString("job_title");
        String employmentStatus = rs.getString("employment_status");
        String hireDate = rs.getString("hire_date");
        BigDecimal salary = rs.getBigDecimal("salary");

        model.addRow(new Object[]{employeeId, department, jobTitle, employmentStatus, hireDate, salary});
    }

    view.setModel(model);
} catch (SQLException e) {
    e.printStackTrace();
    JOptionPane.showMessageDialog(null, "Error fetching data from the database.");
}
    }
```
  
- **>Update (Update Assigned Employee Details):** Implemented by **KEG/IT/2021/F/0090 - Maduranga.**
-  This functionality allows users to update details of employees who are already assigned to tasks or jobs, such as modifying their job roles or assignments.


```
 Connection con = Database.connection();
        try {
            PreparedStatement ptst = con.prepareStatement("UPDATE employment_details SET department=?, job_title=?, employment_status=?, hire_date=?, salary=? WHERE employee_id=?");

          
            ptst.setString(1, txtdepartment.getText());
            ptst.setString(2, txtjobtitle.getText());
            ptst.setString(3, txtemploymentstatus.getText());
            ptst.setString(4, txthiredate.getText());
            BigDecimal salary = new BigDecimal(txtsalary.getText());
            ptst.setBigDecimal(5, salary);
            ptst.setInt(6, Integer.parseInt(txtemployeeid.getText())); 

            // Execute the update query
            int i = ptst.executeUpdate();

            if (i != 0) {
                JOptionPane.showMessageDialog(null, "Employee Details Updated Successfully !");
                showData();
                clear();
            }
        } catch (SQLException e) {
            e.printStackTrace();
            JOptionPane.showMessageDialog(null, "You Must Fill all Fields to Update the Database!!!");
        } catch (NumberFormatException e) {
            System.out.println("Invalid employee ID or salary format.");
        }

  ```
- **>Delete (Delete Assigned Employees):** Implemented by **KEG/IT/2021/F/0120 - Sahan.**
-  This functionality allows users to remove employees from their current assignments or tasks.



```
 Connection con = Database.connection();
    try {
        PreparedStatement ptst = con.prepareStatement("DELETE FROM employment_details WHERE employee_id=?");
        ptst.setInt(1, Integer.parseInt(txtemployeeid.getText()));

        int i = ptst.executeUpdate();

        if (i != 0) {
            JOptionPane.showMessageDialog(null, "Employee Details Deleted Successfully !");
            showData();
            clear();
        } else {
            JOptionPane.showMessageDialog(null, "No employee found with the provided ID.");
        }
    } catch (SQLException e) {
        e.printStackTrace();
        JOptionPane.showMessageDialog(null, "Error deleting employee details from the database.");
    } catch (NumberFormatException e) {
        System.out.println("Invalid employee ID.");
    }
```


*For clarity and professionalism We added Most wanting Code parts, let's avoid embedding all Java function & codes directly.  Please refer to the source file for all code details.* Thank You :) 



## Contribution

**All group members contributed to various aspects of the project**. Apart from the specific functionalities mentioned above, **all members collaborated on UI enhancements, debugging, and fine-tuning of the application.**

## Contributing

Contributions are welcome! If you'd like to contribute to the project, please follow these steps:

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/YourFeature`).
3. Commit your changes (`git commit -am 'Add some feature'`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Create a new Pull Request.

## License

This project is open-source, but it does not include a specific license. You are free to view, modify, and distribute the code as you see fit. However, please note that without a license, there are no explicit permissions or restrictions associated with the use of this software. It is recommended to consult with your legal advisor regarding the usage of this code.
