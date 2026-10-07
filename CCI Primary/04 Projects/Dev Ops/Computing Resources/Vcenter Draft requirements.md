VCenter Provisioning and data collection


Figure out which classes are using vcenter Utilize existing data from the current term in the Academics app.

Estimate how many students are going to be using vcenter to prevent hypervisor overload, we can do this by identifying all of the classes that are using vcenter, right now there is a manual list.  From there we need to get a list and count of all of the students in those classes to determine vlan assignments.

Vlan number allocations for students beings fresh every term it starts at 101-199
200+ is reserved for faculty


Computing Resource?

- Type
    
    - VMWare
        
        - Vlan - We will need to track and assign vlans
            
        
    - ProxMox
        
    - ????
        
- Assigned To
    
    - Student
        
- Class
    
    - Term
        
    - Instructor
        
    - CRN
- Status
	- Pending
	- Provisioned
	- Inactive (Student Drops Class)


## Computer Resource Details
PFSense On VM Ware

CT210-001

Assigned to Jane Doe

Vlan 101 → 199 (Auto Increment). for students Professors will start at 201

Ubuntu On VM Ware

CT210-001

Assigned to Jane Doe

Vlan 101 → 199 (Auto Increment). for students Professors will start at 201

Ubuntu On VM Ware

CT210-001

Assigned to Jane Doe

Vlan 101 → 199 (Auto Increment). for students Professors will start at 201

Ubuntu On VM Ware

CT310-009

Assigned to Jane Doe

Vlan 101 → 199 (Auto Increment). for students Professors will start at 201

- Assigning vlan to resources as the records get created
    

## CSV Export will all information

- Export for all computing resource information

- Incremental daily export with the delta
	- Track when the last time the file was downloaded and then the next export should contain the delta from that time and current time
		- Include date selector, include automated date range but allow user to change it

## Determine Status
- Inactive (Student Drops Class)

## Brian's Notes
VCenter process
- Run delete scripts from previous terms on students and professors
- Remove TA/CA access to resource pools (profs usually retain access)
- Update VCenter and work on any scheduled maintenance
- Create utf8 file from our report
- Check utf8 file for courses that are being taught with scripts for creation
- Generate individual reports per course using (name_of_script)
- Run vm deployment per course on student lists via PowerShell
- Generate prof/TA lists for courses
- Run VM deployment for profs/TAs
- Give TAs and Profs correct access to their resource groups
- Email active professors that provisioning is complete, list the TAs who have access, ask if there are unknown TAs who need access
- TODO: combine scripts so we can just feed it the entire student list 
- TODO: script to predict worst case utilization of limited resources
- TODO: Organize per term/course in folders (storage and non-storage organization)
- TODO: mail merge with instructions on access (?) or maybe make docs for Mike to insert into course shells