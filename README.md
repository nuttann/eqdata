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
relevant, so keep proper nesting for the lines. The reuse of "name"
in each nested map can cause confusion, but it seemed better than
making it longer for both reading the files by humans and programs.

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

