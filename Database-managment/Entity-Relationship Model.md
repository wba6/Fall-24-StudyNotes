# Entity-Relationship Model

## Purpose of E/R Model
- Sketch database schema designs.
- Includes some constraints.
- Later used to convert E/R designs to database schema.

## Entity Sets
- **Entity**: Object.
- **Entity set**: Collection of similar entities (similar to a class in OOP).
- **Attribute**: Property of an entity set; simple values (e.g., integers, strings).

## E/R Diagrams
- **Entity set**: Represented by a rectangle.
- **Attribute**: Represented by an oval connected to its entity set.

## Example
- Entity set **Beers** with attributes **name** and **manf (manufacturer)**.
- Example data: (Bud, Anheuser-Busch).

## Relationships
- Connects two or more entity sets.
- Represented by a diamond with lines connecting to entity sets.

## Example: Relationships
- Bars sell beers.
- Drinkers like beers.
- Drinkers frequent bars.

## Multiplicity of Binary E/R Relationships
- **Many-one**: One entity from the first set is connected to at most one entity from the second set.
- **Example**: A drinker has at most one favorite beer.

## One-One Relationships
- Each entity in one set is related to at most one entity in the other set.
- **Example**: Best-seller relationship between manufacturers and beers.

## Representing “Multiplicity”
- **Arrow**: Shows direction of "one" side.
- **Rounded arrow**: Indicates "exactly one".

## Many-Many Relationships
- An entity from either set can be connected to many entities of the other set.
- **Example**: A bar sells many beers, and a beer is sold by many bars.

## Attributes on Relationships
- Sometimes attributes are attached to relationships.
- **Example**: Price as an attribute of the relationship between bars and beers.

## Multi-way Relationships
- Connects more than two entity sets.
- **Example**: A drinker may prefer certain beers at certain bars.

## Roles
- An entity set can appear more than once in a relationship with roles labeled on edges.

## Subclasses
- **Subclass**: Special case with fewer entities and more properties.
- **Example**: Ales as a subclass of beers with an additional attribute, color.

## Keys
- A set of attributes for an entity set that uniquely identifies entities.
- Underline key attributes in E/R diagrams.

## Weak Entity Sets
- Entities needing support from other entity sets to be uniquely identified.
- Represented with double rectangles and double diamonds for relationships.

## Design Techniques
1. Avoid redundancy.
2. Limit the use of weak entity sets.
3. Use attributes when appropriate instead of entity sets.

## Avoiding Redundancy
- Redundancy wastes space and causes inconsistencies.

## From E/R Diagrams to Relations
- **Entity set** → **Relation**.
- **Relationships** → Relations with keys and attributes of connected entity sets.

## Subclasses: Three Approaches
1. **Object-oriented**: One relation per subclass with all attributes.
2. **Use nulls**: One relation with NULLs for non-relevant attributes.
3. **E/R style**: One relation for each subclass with key attributes.

## Exercises
- Create models for single and multiple entity sets.
- Refine E/R diagrams to reduce data redundancy.
