
## 2.2 - Rebrand And Multi School Support
Project creation and update:
- Users are now able to select College, 
- Project browsing now supports richer filtering and better navigation: year, school, category, advisor, project title, and team member search.
- The gallery now loads all projects by default on first page load instead of automatically limiting to the active competition year.
- Project detail pages were redesigned and now include stronger metadata, structured data, and improved presentation of related content to match to revise site styles.

Project idea creation and update:
- The idea creation form was improved substantially.
- Users can create a new stakeholder directly from the idea form and optionally upload a stakeholder headshot/avatar.
- Users can create a new advisor directly from the idea form and optionally upload an advisor avatar.
- The advisor and stakeholder modal dialogs were hardened so they behave more reliably in the page.
- The competition dropdown on the idea form was simplified to show the competition name rather than a year-name combined label.

**Project and Showcase Features**
Project awards and winners:
- Added a new `ProjectAward` model to represent first place, second place, third place, and honorable mention awards.
- Added admin support for managing project awards.
- The homepage now highlights first-place winners by school for the active competition. We are not actively using this but this feature will be available for this years competition
- Added a new school-specific winners page so users can browse all winners for a school within a competition.We are not actively using this but this feature will be available for this years competition
- Past winners content and winners presentation were redesigned.

Project discovery and browsing:
- The project gallery was reworked to support server-rendered initial results plus dynamic filtering/pagination.
- Added pagination URLs, filter-state URLs, active filter chips, and clearer navigation behavior.
- Sorting options now include title, last updated, and year.
- The gallery initial load behavior was changed so all projects display by default rather than only the active competition.

Homepage and public-facing content:
- Branding has been updated the primary navigation is now using the new COEC logo, each school section is using the new School name and new School logos
- The homepage was fully redesigned with a new hero section, school cards, featured projects, winner highlights, and a stronger visual identity.
- Schools now support richer marketing content and styling through new fields:
- About, Student Resources, Sponsors, Judges, Instructions, Past Winners, and project detail/index pages all received major redesigns.
- Public pages and project detail/gallery pages now include better metadata for indexing and sharing.  We will continue building this out as we go.


## Release 2.3 Project Idea Adoption Related Updates
Added Competition Ideas Release Date
	- Idea release data controls student access to Project Idea list page and Project Idea detail page and Project Idea nav link.
- Added Delete and Edit Project Idea functionality for admin users 
- Added School filtering to Project Idea List page
- Project Ideas sorted alphabetically on list page
- Fixed project idea document validation
- Enter/Return no longer submits the Project Idea form
- Added Minimum and Maximum Team Member attributes to project idea
- Added Team member selection to the project idea page, students now must add all of their team members to their team before claiming the project idea.
- All dropdowns and multiselects are now using the School slug (SCIS, etc...) instead of the full school name
- Added acknowledgement that students must accept before claiming a project, this is from Tech Transfer/OGC per Marie "I understand that I am not required to work on an external sponsor’s project and may instead pursue an approved entrepreneurial project."


