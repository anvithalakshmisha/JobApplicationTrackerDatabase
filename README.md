##Database Topic:
Job Application Tracker
##Database purpose:
The purpose of the database is to maintain the data of job applicants and use it to track job applications, including job listings, application status, interview dates, and company information.
Business problem solved:
The designed database caters to the efficient management of a job application system. 
1.	It enables streamlined talent acquisition by organizing applicant profiles, skills, education history, and documents. 
2.	The system facilitates a smooth job application process, allowing for effective tracking and evaluation of applications and interview details. 
3.	Job listings and associated information are managed systematically, promoting an organized job posting system. 
4.	Automated document management reduces administrative efforts and enhances document security. 
5.	The database supports communication between recruiters and candidates, fostering collaboration and a personalized applicant experience. Through data analysis, it aids in data-driven decision-making, compliance reporting, and recruiter performance evaluation. 
6.	Ultimately, the database empowers organizations to make informed decisions, optimize recruitment strategies, and effectively select candidates, contributing to efficient talent management and successful recruitment endeavors.

Business requirements:
1. Each company can have 0 or more job listings 
2. Each company must have one or more recruiters 
3. Each applicant must have one or more education history 
4. Each applicant can have 0 or many applied jobs 
5. Each applicant can have 0 or many saved jobs 
6. Each applicant must have 1 profile 
7. Each applicant can have 0 or many skills and documents 
8. Applied jobs and saved jobs can have 0 or many job listings 
9. Each applied jobs must have an application status and 0 or many interviews
10. Each company must have one address
11. Each applicant must have one address
12. Each recruiter can have 0 or more job listings
13. Each job listing must have one recruiter

Design decisions:

 No.	Entity	Attributes	Design Decisions	Relationships
1.	Job Applicant	ApplicantID (PK), FirstName, LastName, Email, PhoneNumber, AddressID (FK)
	•	The Job Applicant entity stores information about individuals applying for jobs. 
•	The AddressID is a foreign key to the Address entity, linking each applicant to an address. 
•	This separation of concerns helps maintain data integrity and prevents duplication of address details.	Related to Address (FK), Applicant Profile, Applicant Skills, Applicant Education, Applicant Documents, Saved Jobs, Applied Jobs.

2.	Applicant Profile	ProfileID (PK), ApplicantID (FK), Profile Picture, Summary	•	This entity stores additional profile-related information for job applicants. 
•	It's linked to the Job Applicant entity to maintain a one-to-one relationship and store applicant profiles.
	Linked to Job Applicant (FK).
3.	Skill	SkillID (PK), SkillName	•	Skill entity stores various skills, and it's linked to Applicant Skills to associate specific skills with job applicants.
	Related to Applicant Skills.
4.	Applicant Skills	ApplicantSkillID (PK), ApplicantID (FK), SkillID (FK)	•	This junction table establishes a many-to-many relationship between Job Applicant and Skill entities, allowing applicants to have multiple skills.	Linked to Job Applicant (FK) and Skill (FK).

5.	Education History	EducationID (PK), Degree, Institution, FieldOfStudy, GraduationYear	•	Education History stores educational details and is linked to Applicant Education to maintain a clear separation and association of educational history.
	Related to Applicant Education.
6.	Applicant Education	ApplicantEducationID (PK), ApplicantID (FK), EducationID (FK)	•	This junction table represents the many-to-many relationship between Job Applicant and Education History, allowing applicants to have multiple educational records.
	Linked to Job Applicant (FK) and Education History (FK).
7.	Document Type	DocumentTypeID (PK), DocumentType	•	Document Type entity stores types of documents, and it's linked to Applicant Documents to categorize various applicant documents.
	Related to Applicant Documents.
8.	Applicant Documents	ApplicantDocumentID (PK), ApplicantID (FK), DocumentID (FK), DocumentPath	•	This entity stores applicant-specific documents with their types, allowing efficient management and retrieval of documents for each applicant.
	Linked to Job Applicant (FK) and Document Type (FK).
9.	Address	AddressID (PK), Street, City, State, ZipCode, Country	•	Address is a separate entity to avoid redundancy in storing address information for job applicants and companies. 
•	It promotes normalization and efficiency.
	Related to Job Applicant and Company Information through foreign keys.

10.	Job Listings	JobID (PK), JobTitle, Description, Location, SalaryRange, EmploymentType, ExperienceLevel, CompanyID(FK)	•	Job Listing entity represents job postings with relevant details, and it's linked to other entities to track saved jobs, applied jobs, and interviews associated with each job listing.	Related to Saved Jobs, Applied Jobs, Interview.
11.	Company Information	CompanyID (PK), CompanyName, AddressID (FK), Industry, ContactEmail, ContactPhone	•	Company Information entity represents information about companies, and it's linked to Address and Job Listing to maintain accurate company details in the system.
	Related to Address (FK), Job Listing, Recruiters.

12.	Saved Jobs	SavedID (PK), ApplicantID (FK), JobID (FK)	•	This junction table establishes a many-to-many relationship between Job Applicant and Job Listing, allowing applicants to save multiple job listings.
	Linked to Job Applicant (FK) and Job Listing (FK).
13.	Application Status	ApplicationStatusID (PK), StatusDescription
	•	Application Status entity stores status descriptions for job applications, providing information on the application status.
	Related to Applied Jobs.
14.	Applied Jobs	ApplicationID (PK), ApplicantID (FK), JobID (FK), ApplicationDate, ApplicationStatusID (FK)
	•	This entity represents job applications, linking applicants to job listings and storing application-related details.
	Linked to Job Applicant (FK), Job Listing (FK), Interview.

15.	Interview	InterviewID (PK), ApplicationID (FK), InterviewDate
	•	The Interview entity represents interview details linked to job applications, allowing tracking of interview-related information.	Linked to Applied Jobs (FK).
16.	Recruiters	RecruiterID (PK), CompanyID (FK), FirstName, LastName, Email, Phone
	•	Recruiters entity stores information about recruiters associated with companies, linked to Company Information for accurate representation of recruiters.
	Related to Company Information (FK).


Key Design Decisions:

Key design decisions in this database include:
•	Utilizing a relational database management system to ensure data integrity, consistency, and easy querying.
•	Employing appropriate indexing for efficient querying, especially on frequently accessed attributes like ApplicantID and JobID.
•	Ensuring normalization up to 3rd Normal Form to minimize data redundancy and maintain data consistency.
•	Utilizing foreign keys to establish relationships between entities and ensure referential integrity.

Conclusion:

This database design addresses the business problem of efficiently managing job applications, listings, interviews, and related data. By organizing the entities and their relationships, and adhering to normalization principles, this database aims to provide a robust foundation for an effective job application platform.
