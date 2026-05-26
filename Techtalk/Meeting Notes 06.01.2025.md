

weight wird umgesetzt
Comments müssen auch noch auf der maske 


# PR Status — Stand: 09.01.2026
### Reminder: Understand the goal of this PR first, then work on it.

## Done
- I have added @kcinay055679 implementation of the generic table.
- I refactored to fill the data into the table correctly using the new generic-cv component.
- I wrote some first Models that should be able to get the overview.
- I wrote the getMemberOverview and put mock date into it until we have the real backend.

## ToDos
- [ ] rewrite the Models to hold the right data. (the methode with the data is exactly what needs to be dispalyed)
- [ ] Ask the Ux Team if the Tabbar is what they expect it to look like

## Additional information to move forward
Some tables expect there to be a field which has the tow dates (start-  and enddate) in a combined format
<img width="222" height="182" alt="Screenshot from 2026-01-09 16-39-36" src="https://github.com/user-attachments/assets/0a534c65-0733-4e0a-a266-fd9353fab689" />
Therefor we have to 

## Open Questions / Risks (if any)
- 


Any special-case or conditional logic must be documented in the PR with comments on the code segments. 