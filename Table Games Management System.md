

# High-level breakdown
Table Games Management System that provides
- Dashboard with birds-eye view of the pit
	- Point-and-click functionality to view the details of an active table, or to open a closed table.

- What type of data needs to be displayed at a glance?
	- Tables that are active, and inactive.
	- Seats that are occupied, and seats that are not occupied.
	- An occupancy count displayed on the table.
	- A rough shape of the pit should be displayed, to give an interactive experience.
	- There should be a main modal
		- Total # of active players
		- Total # of players for day
		- Total amount of buy-ins
		- Total amount of cash-outs
		- Pit Bosses
	- Date and time should be displayed somewhere.

- What type of data should be displayed when you click on a table?
	- Active Dealer
	- Next Dealer
	- Total Players Active on this Table
	- Total Players for Day on this Table
	- Total Buy-Ins on this table
	- Total Cash-Outs on this table
	- Table Minimum
	- Table Maximum
	- Chip Fill
	- Chip Credit
	- Player Buy-In
	- Player Cash-Out

- Where are we going to store information like default tray amounts that we can fill to on these tables?
	- I want to be able to automatically request a fill for the specific amount that will fill that specific table to the default filled tray amount defined probably by the table min/max to ensure that the correct denominations are used on tables with higher/lower limits.

- What type of information does the dealer rotation need to show?
	- Should display the attributes that each dealer has (what games they are able to deal)
	- Dealer assignment is still pit bosses discretion.


- Are we considering a dealer check-in screen at shift start?
	- Pit boss does a roll call on employees, inputs available dealers into the rotation builder system.

- What is the workflow going to look like for the pit boss?
	- Check dealers in
	- Assign Dealers to Tables
	- Allow modification to Dealer rotation
	- Open table, verify that closing amount matches opening amount
	- Buy players in/ Cash Players out
	- Fill Tables, Credit Tables
	- Close Table
	- View player records, table records, dealer records.


- What does the dealer rotation screen need?
	- Should be able to create separate rotations for different sections of the pit depending on the number of dealers available and the amount of tables that are open.
	- I want to be able to allow there to be a craps rotation, and also multiple blackjack rotations, because blackjack dealers will likely do 2 tables in a rotation, then go to break, then have to go to 2 more tables on the other side of the pit.
# Data Models

- Dealer
	- Name
	- Shift
	- Badge #
	- Current Table
	- Skills
		- List tables that the dealer can deal


- Player
	- Name
	- DOB
	- Height
	- Weight
	- Driver's License Number
	- Player History
		- Buy-In History
		- Cash-Out History
	- Currently Playing

Table
	- Game Name
	- Table Minimum
	- Table Maximum
	- Tray Amount
	- Current Players
	- Total Players for Day


- Title 31 / Bank Secrecy Act
	- CTRs
	- MTLs

- NIGC Minimum Internal Control Standards
	- Dictates the required fields and standards for all the things that will be needed
	- Separate gapless sequences for fills and credits
	- One active series per slip type, enforced in the database
	- Slips are immutable once issued; corrections happen through void records with reason, user and timestamp
	- Three copies with role-based custody, the restricted copy inaccessible to the cage and pit
	- A sequence-gap and duplicate audit report
	- A full audit log of who created, signed, transported, and received each slip
