# sql-challenge

## Instructions
This Challenge is divided into three parts: data modeling, data engineering, and data analysis.

## Data Modeling
Inspect the CSV files, and then sketch an Entity Relationship Diagram of the tables.
![QuickDBD-Challenge_9](https://github.com/JuanTenopala/sql-challenge/assets/144553115/9d44f7a5-cee2-42f1-b63e-9f2214ac53a1)
Link to schema: https://app.quickdatabasediagrams.com/#/d/mKZran

## Data Engineering
Use the provided information to create a table schema for each of the six CSV files.

-- Drop Tables
DROP TABLE IF EXISTS employees;
DROP TABLE IF EXISTS departments;
DROP TABLE IF EXISTS titles;
DROP TABLE IF EXISTS dept_emp;
DROP TABLE IF EXISTS salaries;
DROP TABLE IF EXISTS dept_manager;

-- Exported from QuickDBD: https://www.quickdatabasediagrams.com/
-- Link to schema: https://app.quickdatabasediagrams.com/#/d/mKZran

CREATE TABLE "titles" (
    "title_id" VARCHAR(50)   NOT NULL,
    "title" VARCHAR(50)   NOT NULL,
    CONSTRAINT "pk_titles" PRIMARY KEY (
        "title_id"
     )
);
SELECT * FROM titles

CREATE TABLE "departments" (
    "dept_no" VARCHAR(50)   NOT NULL,
    "dept_name" VARCHAR(50)   NOT NULL,
    CONSTRAINT "pk_departments" PRIMARY KEY (
        "dept_no"
     )
);
SELECT * FROM departments


CREATE TABLE "employees" (
    "emp_no" INT   NOT NULL,
    "emp_title_id" VARCHAR(100)   NOT NULL,
    "birth_date" VARCHAR(100)   NOT NULL,
    "first_name" VARCHAR(100)   NOT NULL,
    "last_name" VARCHAR(100)   NOT NULL,
    "sex" VARCHAR(100)   NOT NULL,
    "hire_date" VARCHAR(100)   NOT NULL,
    CONSTRAINT "pk_employees" PRIMARY KEY (
        "emp_no"
     )
);
SELECT * FROM employees

CREATE TABLE "dept_manager" (
    "dept_no" VARCHAR(50)   NOT NULL,
    "emp_no" INT   NOT NULL
);
SELECT * FROM dept_manager

CREATE TABLE "salaries" (
    "emp_no" INT   NOT NULL,
    "salary" INT   NOT NULL
);
SELECT * FROM salaries

CREATE TABLE "dept_emp" (
    "emp_no" INT   NOT NULL,
    "dept_no" VARCHAR(50)   NOT NULL
);
SELECT * FROM dept_emp

ALTER TABLE "employees" ADD CONSTRAINT "fk_employees_emp_title_id" FOREIGN KEY("emp_title_id")
REFERENCES "titles" ("title_id");

ALTER TABLE "dept_emp" ADD CONSTRAINT "fk_dept_emp_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

ALTER TABLE "dept_emp" ADD CONSTRAINT "fk_dept_emp_dept_no" FOREIGN KEY("dept_no")
REFERENCES "departments" ("dept_no");

ALTER TABLE "salaries" ADD CONSTRAINT "fk_salaries_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

ALTER TABLE "dept_manager" ADD CONSTRAINT "fk_dept_manager_dept_no" FOREIGN KEY("dept_no")
REFERENCES "departments" ("dept_no");

ALTER TABLE "dept_manager" ADD CONSTRAINT "fk_dept_manager_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");


