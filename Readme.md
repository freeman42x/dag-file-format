# DAG file format

Can be used to describe in a minimal and readable fashion a Directed Acyclical Graph (DAG).

## Format specification

1. **File Structure**: A `.dag` file is a text file where each line represents a node in the DAG. Nodes are organized in a hierarchy, and their position in the hierarchy is indicated by their indentation level. The root nodes of the DAG have no indentation, and each additional level of indentation indicates a step down in the hierarchy.

2. **Indentation**: Indentation is used to denote the level of each node in the DAG. Each indentation level is represented by a tab character (`\t`). A node with no leading tab characters is a root node. A node with one leading tab character is a child of the nearest preceding node with one less tab character, and so on.

3. **Duplicate Names**: Nodes can have duplicate names, but each parent-child relationship must be unique. That is, if "Sales" is a child of both "CEO" and "CFO", then those are considered distinct nodes.

4. **Acyclic Condition**: The graph represented by the `.dag` file must be acyclic. This means that there must be no sequence of parent-child relationships that leads from a node back to itself.

5. **Line Termination**: Each node is terminated by a newline character (`\n`).

Here is a formal Backus-Naur Form (BNF) representation of the `.dag` file format:

```
<dag> ::= <node>
<node> ::= <level><name><line-end><node> | <empty>
<level> ::= <tab><level> | <empty>
<name> ::= <non-tab-char><name> | <non-tab-char>
<line-end> ::= '\n'
<tab> ::= '\t'
<non-tab-char> ::= any character that is not a tab
<empty> ::= ""
```

Example `.dag`

```
CEO
	Operations
		Logistics
			Manager1
		Manufacturing
			Manager2
				Supervisor
	Sales
		Domestic
			Manager3
CFO
	Sales
		International
			Manager4
	Operations
HR
	Manager3
		TeamLead
```