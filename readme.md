Following tutorial from Gavin Lon<br>
Link: https://www.youtube.com/playlist?list=PL4LFuHwItvKbzDl6MBp3XY0MrnALSfyub


# Part 1 - Introduction
## Project related to this
- `TCPData`
- `TCPExtension`
- `ThePretendCommpanyApplication`
## Some summary
- Class extension and Lambda expression
- IEnumerable and IQueryable
- Create class extension filter and try it to filter list of `Employee` and `Department`
- Use already defined extension in `Linq`, `Where`
- sql-like query syntax provided by `Linq`, but some query still need to use extension method provided by `Linq`

# Part 2 - Queries
## Project related to this
- `LINQExamples_1`
## Some summary
- Method Syntax and Query Syntax
- `Select` method syntax 
    ```
    var results = employeeList.Select(e => new
            {
                FullName = e.FirstName + " " + e.LastName,
                AnnualSalary = e.AnnualSalary
            });


    // with chaining
    var results = employeeList.Select(e => new
            {
                FullName = e.FirstName + " " + e.LastName,
                AnnualSalary = e.AnnualSalary
            }).Where(e => e.AnnualSalary >= 50000);


    ```
- `Select` Query Syntax
    ```
    var results = from emp in employeeList
              select new
              {
                  FullName = emp.FirstName + " " + emp.LastName,
                  AnnualSalary = emp.AnnualSalary
              };

    
    // with where clause
    var results = from emp in employeeList
              where emp.AnnualSalary >=50000
              select new
              {
                  FullName = emp.FirstName + " " + emp.LastName,
                  AnnualSalary = emp.AnnualSalary
              };
    ```
- Deffered and Immediate Execution<br>
    Immediate execution with "To conversion method"  
- `INNER JOIN` using operator `JOIN` Method Syntax
    ```
    var results = departmentList.Join(employeeList,
    department => department.Id,
    employee => employee.DepartmentId,
    (department, Employee) => new
    {
        FullName = Employee.FirstName + " " + Employee.LastName,
        AnnualSalary = Employee.AnnualSalary,
        departmentName = department.Longname
    });
    ```
- `INNER JOIN` using query syntax
    ```
    var results = from dept in departmentList
              join emp in employeeList
              on dept.Id equals emp.DepartmentId
              select new
              {
                  FullName = emp.FirstName + " " + emp.LastName,
                  AnnualSalary = emp.AnnualSalary,
                  departmentName = dept.Longname
              };
    ```
- `LEFT OUTER JOIN` using `GroupJoin` operator
    ```
    var results = departmentList.GroupJoin(employeeList,
    dep => dep.Id,
    emp => emp.DepartmentId,
    (dept, employeesGroup) => new
    {
        Employees = employeesGroup,
        DepartmentName = dept.Longname
    });
    ```
- `LEFT OUTER JOIN` using `into` keyword and `join`
    ```
    var results = from dept in departmentList
              join emp in employeeList
              on dept.Id equals emp.DepartmentId
              into employeeGroup
              select new
              {
                  Employees = employeeGroup,
                  DepartmentName = dept.Longname
              };
    ```