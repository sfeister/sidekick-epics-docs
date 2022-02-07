# Creating an IOC in EPICS (CentOS)

Used the following resource: https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html



Step 1:

Within your EPICS folder, prepare a file called 'test.db'. 

Inside, copy the following:

```
record(ai, "temperature:water")
{
    field(DESC, "Water temperature in the fish tank")
}
```

This file creates a record. A reccord database is how EPICS is used, through these files. The record is called "temperature:water" and has an analog input (ai). The field "DESC" stands for the description of the record. Later on, you will have many more fields to work with and add information to your database. 

Step 2:

After you save and close your new file, close the terminal and open a new one. 

```
softIoc -d test.db
```

Step 3:

After this, you will see the EPICS prompt open, like so:

```
epics>
```

Now, type in "dbl". Then, the record name will display.

```
epics> dbl
temperature:water
epics>
```

Step 4:

Open another terminal. Try this line. 

```
caget temperature:water
```

This should display:

```
temperature:water 0
```

Step 5:

Within the same terminal, try the following line:

```
caput temperature:water 6
```

This should display:

```
Old: temperature:water         0
New: temperature:water         6
```

Step 6:

You can try the 'caput' function again, or you could open another terminal and try this line:

```
camonitor temperature:water
```

Then, as you go back to Terminal #2, you can try 'caput' a few more times and see as Terminal #3 changes each time. 


