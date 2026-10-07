# Spring 2026

  

**Points:** 20 extra credit points

**Submission:** One SQL script and one screenshot or PDF showing the final verification output

**Important:** You must complete the entire assignment to receive any points. Partial credit will not be awarded for incomplete assignments. There is no companion sql file for this assignment. You must write the entire solution yourself in a single SQL script.

  

## Assignment Overview

  

Build a small but complete database solution for a **customer service ticket system**. Your work must include:

  

- table creation

- data insertion

- a function

- a stored procedure

- a view

- a trigger

  
  

## Required Scenario

  

Your database must model a customer support workflow using these four entities:

  

- `Customers`

- `Technicians`

- `ServiceTickets`

- `TicketAudit`

  

## Required Technical Work

  

Your SQL script must perform all of the following:

  

1. Create the four required tables listed above.

2. Use appropriate primary keys and foreign keys.

3. Insert enough test data to demonstrate the workflow.

Minimum required data:

`Customers`: 3 rows

`Technicians`: 2 rows

`ServiceTickets`: 5 rows

4. Create a view named `vw_TicketSummary`.

The view must join at least `Customers` and `ServiceTickets`.

5. Create a function named `fn_OpenTicketCount`.

The function must accept a customer identifier and return that customer's number of open tickets.

6. Create a stored procedure named `sp_CloseTicket`.

The procedure must accept a ticket identifier and a resolution note, then mark the ticket as closed.

7. Create a trigger named `trg_TicketClosedAudit`.

When a ticket changes from not closed to closed, the trigger must insert a row into `TicketAudit`.

8. End the script with test statements that clearly prove each object works.

  

## Workflow Expectation

  

Your objects must operate as one connected workflow:

  

- the base tables store the support data

- the stored procedure closes a ticket

- the trigger records that closure in the audit table

- the function reports open ticket counts

- the view summarizes the data for reporting

  

If the required objects do not work together, the solution will not receive full credit.

  

## Submission Requirements

  

Submit the following:

  

1. One SQL script that runs from top to bottom. I will take the entire script and run it in a clean database environment. The script must create all tables, insert all data, create all objects, and include the final verification statements. If it does not run without error you will not receive credit.

2. One PDF showing the output of your final verification statements.

  

Your SQL script must include:

  

- brief comments labeling each major section

- all required `CREATE` and `INSERT` statements

- the test statements used to verify the finished solution

  

## Final Verification Section

  

At the end of your script, include SQL statements that clearly show:

  

1. The inserted base data from `Customers`, `Technicians`, and `ServiceTickets`

2. The result of calling `fn_OpenTicketCount` for at least one customer before and after closing a ticket

3. The execution of `sp_CloseTicket`

4. Evidence that `trg_TicketClosedAudit` inserted a new row into `TicketAudit`

5. The output of `vw_TicketSummary`

  

The grader should be able to run your script and inspect the results without guessing what to check.

  
  
  

# Grading Guidelines

  

## Restrictions

  

- Do not submit separate files for each object.

- Do not submit a partially manual process that requires the grader to invent test data.

- Do not rename the required tables or required database objects.

- Do not build unrelated examples for the function, procedure, trigger, and view.

  

## Grading Rubric (20 Points)

  

- **4 points:** Tables are well-structured and correctly related

- **3 points:** Inserted data is sufficient and supports meaningful testing

- **3 points:** View is correct and useful

- **3 points:** Function works and returns a meaningful calculated result

- **4 points:** Stored procedure performs a valid multi-step workflow

- **3 points:** Trigger fires correctly and its effect is visible in the final output

  

## Grading Notes

  

Make the grading obvious. If the grader cannot quickly locate `vw_TicketSummary`, `fn_OpenTicketCount`, `sp_CloseTicket`, `trg_TicketClosedAudit`, and the final test output, points will be lost even if parts of the solution are technically correct.