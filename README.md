# raapl

`raapl` is an educational implementation of Relational Algebra in APL.

I started it as a response to a Python project [rashell](https://github.com/skebir/rashell).

The aims are
1. to provide an environment in which to explore RA (Relational Algebra) as 
   originally described in Codd's [1969 paper](https://technology.amis.nl/wp-content/uploads/images/RJ599.pdf), and
2. to illustrate the power of ⍳, ∊ and compression to those unfamiliar with APL.

The implementation is unconcerned with efficiency, and the APL is written in a style that I hope will be readily understandable to novice readers.

At present the implementation covers Relations and a few of the relational 
operators.

**NB:** Here `operator` is used in the RA sense, not the APL sense!

## Limitations

### Temporary

1. Some Relational Operators are not yet implemented.
2. Insert and Project do not yet enforce uniqueness on the tuples.
3. Creation does not yet check that Field names are acceptable.
4. Constraints are not yet implemented. When they are they will probably exist within a schema which will also contain Relations.
5. RA does not discuss persistence of definitions or data, but it is clearly a desirable feature. At present the only persistence mechanism is the workspace.


### (Probably) Permanent

`raapl` is not fully consistent with RA.

`raapl` has reserved words which cannot be used as Field names since the names 
would clash with properties of the Relation.

RA is based on [Set Theory](https://en.wikipedia.org/wiki/Set_theory). The elements of Sets are unique within the Set that contains them, and they are unordered.

`raapl` **will** implement the uniqueness constraint since this affects how the Insert and Project operations work.

However, `raapl` **will** order Fields and their values, since they are held in APL arrays, and it seems perverse to deliberately shuffle them.

This has an advantage. RA distinguishes between a Relation and a Table; a Table is the form in which a Relation is displayed, and its rows and columns are inevitably ordered. Since the Fields and Values in `raapl` are ordered it is possible to display Relations directly.

## Installation and use

I have not yet written installation instructions since the initial reviewers 
are all likely to be users of Dyalog APL.

### Use

1. Open RIDE using the project root as the working directory
2. Create relations by invoking `r ← <name> relation <field_1> <field_2> ....<field_n>`. That will create an instance of a subclass of Relation, with the Fields available as read-only properties.

### Relational operators

These are methods defined in `Relation`.

1. `Insert` inserts a row of data into the relation.
2. The _structure_ of Relations is immutable, so all other operators create new relations.
3. `Project` creates a new relation with a subset of the original 
   relation's fields.
4. `Display` is a method that is not one of the original Operators. It returns a table which reflects the structure and contents of the Relation.
5. `Rows` is a helper method that returns a scalar count of the tuples in 
   the relation.

### Tests

Run `test_all` to run all the current automated tests.

Feedback is welcome, as are offers to contribute. I am working on this as a fun 
project on Friday mornings, so the code will develop slowly.

