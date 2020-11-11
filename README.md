# Everquest Data Files

The files here are populated with data extracted from various sources.
Some are entered by hand while others are extracted by programs from
various sources. The data could be useful by programs written in any
language so are in a separate repository than the programs that first
were written to interact with these.

## quest_data.yml

The quest_data.yml file contains info describing collection quests. The
format is a nested set of maps.


```YAML
- name: Rain of Fear
  zones:
    - name: Shard's Landing
      quests:
        - name: A Tracker's Guide to Shard's Landing
          ids: 77376...77388
          note: Ground - Outer ring
        - name: Alarans in Chains
          ids: 77424...77431
          note: Drop - Alaran's
```

The data for this file was entered by hand. The IDs were obtained by
pulling them from files created by "/output inventory", 
"/output realestate", and the various loot filter files.

The format consists of a nested array of maps. Nesting in YAML is
relevant, so keep proper nesting for the lines. 

Most of the entries are straight forward.

The inner array of quests has three fields.

```
name: The name of the quest.
ids: The item IDs associated with this quest.
note: Info on how these are obtained.
```

The "ids" field is a string describing the numbers for the quest items. It
is a comma-separated list of ID numbers or ranges. At the time of this
documentation, every quest except one could be described with a simple
range. The "Bat Attack" quest in Nagafen's Lair has one ID not in
sequence, so this extended notation was used. (E.g.,
"ids: 81717...81723,81756")

One way that works for a new expansion is to examine the collection achievements
for a new expansion. From that you can gather the expansion, zone, and quest
names. In addition, looking at the quests you can see the number of items for
each quest. What is missing from that information is the item ID numbers and
any information as to any details as to how to acquire the drops.

So for the start of the Rain of Fear quest listed above, this is what was
initially entered:

```YAML
- name: Rain of Fear
  zones:
    - name: Shard's Landing
      quests:
        - name: A Tracker's Guide to Shard's Landing
          ids: 1...13
          note: 
        - name: Alarans in Chains
          ids: 1...8
          note: 
```

Since there were 13 items for the first quest and 8 items for the second, the ID
numbers were temporarily set to 1-13 and 1-8. EQ does not appear to use ID
numbers lower than 1001.  This just gives the correct number of items in the
expanded list and all the names will show as "???" until this is changed.

When an item is found for one of the quests, get its ID number. This can be done
by getting it from files created by "/output inventory", "/output realestate",
or by setting it to always need or always greed in the loot filter and checking
the appropriate loot filter file. Other sources such as Allakhazam can be
checked to get one of the item numbers once it is collected there.

Once you have one number, the range of numbers can be guessed by assuming that
they are sequential numbers in the same order as listed in the achievement list.
From there, guess the beginning and end of the range.

For example:

If the third item in the list is found to be 77378, then subtract 2 to get the
1st number of 77376 and then since that quest has 13 items, add 12 to the first
number to get the last number of 77388. The range then becomes 77376...77388. That can be now entered for the "ids" field.

As names are gathered over time in the itemdb.yml file, the listing will start
populating them. The range was only a guess, so check the listing to see that
the names do match up with the expected names. It is always possible that some
new quests may end up with items that are not in the expected sequence. But,
other than Bat Attack, everything has been sequential.

The notes section is optional, but has been useful to people when out gathering
items. As information is found about how to get the items, it can be added in
that line.

## itemdb.yml

The itemdb file contains currently used data for items. The format is
a map of item entries.

Example data

```YAML
0:
  name: Empty
  iconid: 0
1001:
  name: Cloth Cap
  iconid: 639
1002:
  name: Cloth Veil
  iconid: 677
```

The format is a simple map of ID numbers to item maps containing "name" and
"iconid" fields.

Note: Names have changed over the years. Some names may have been changed, but
just not been extracted from files since the change. Also, loot filters are
only updated when that item is seen, so could actually contain old information.
The two inventory files produced by "/output" should be totally current as of
when the command was executed. But since this file was created with a mix
of loot filter files, dumped files and some older sources, some names may be
old.

Note: The ID 0 is not associated with an item. The name "Empty" comes from
the "/output inventory" command.  It could have been special cased, but might
come in useful. This could be changed at a later date if it makes sense.

Technically, this could be updated by hand for new items. This is best kept
consistent using programs to extract the data from authoritative sources such as
"/output inventory", "/output realestate", and loot-filter files. Other sources
would be using a program to grab an item name for an ID from something like
Allakhazam.  The repository [equtils](https://github.com/nuttann/equtils) has a program
"updateiteminfo" that can extract the names from the EQ-generated text files
listed above.
