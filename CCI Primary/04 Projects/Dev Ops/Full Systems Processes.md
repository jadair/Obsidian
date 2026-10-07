Account Creation Pain Points

- TA info not clean from Melissa - either script cleaning or get data from a better source
- Need to filter the Accudemia output to only courses with TAs listed (from above file)


Fields missing in Tom's report:

"Course","Crn","Ptrm Start Date","Ptrm End Date","Course Title","Stu Email Address2"
Note: eligible but not enrolled students should be in the card access file, but this does not include abc123
Card access file does not have emeritus faculty in it

Accudemia - NOW IN BOOKSTACK
https://bookstack.cci.drexel.edu/books/account-management/page/accudemia/

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




Card Access - Check for New Users
- Take last term file and new term file, separate out only userid column and sort
- comm -13 {{old_term_userids}} {{new_term_userids}} > {{new_student_ids}}
- for i in $(cat {{new_student_ids}}); do cat {{new_term_cards}} | grep $i >> {{output_file}}; done




What do we do each term?

- Update CCI Commons employee Access 
	- AD Updates
	- Tux updates
	- CCure (Drexel)
	- CCure (3675, includes Mailroom access)
	- (work on list of them)(not yet done for WI24)
- Archive and unarchive Tux home directories (work in progress)
- Create Tux accounts
- Syncrhonize Snipe-IT accounts (based on Tux)
- VCenter VM deployment
- Accudemia account/course provisioning
- Tux upgrades (work needed but not in progress)
- Ceph upgrades (work needed but not in progress)
- Proxmox upgrades (work needed but not in progress)
- Discord account creation (automated save for TA assignments)
- Annual - install new Matlab release on Tux
- AV Upgrades and Repairs
- VCL
- Oracle
- AWS for Senior Design (Fall/Spring/Summer)
- Boson NetSim (net security 2) (check if running WI24)
- CLC TV website
- MongoDB/MariaDB/ElasticSearch (specific classes)




New Fac/Staff To-Do
- Tux account
- AD groups
- Snipe-IT