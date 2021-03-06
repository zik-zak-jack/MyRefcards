# JPA

## ORM Impedance MisMatch

Mismatch				|	Explanation	
------------------------|---------------
Granularity MisMatch	|	Object Model is more granular than the Relational Model
Inheritance MisMatch	|	Inheritance hierarchy is in Object Model but not in Relational Model
Identity MisMatch 		|	Object Identity & Equality concepts in Object Model vs Primary Key constraint in Relational Model
Association MisMatch	|	Object References in Object Model vs Foreign Key references in Relational Moadel
Data Navigation			|	Navigate the Object graph vs SQL Joins

## Aggregation & Composition

- Aggregation : When the whole is destroyed, its parts are not destroyed. E.g., When the Band is destroyed, its Artists are not destroyed
- Composition : When the whole is destroyed, its parts are also destroyed. E.g., When the House is destroyed, its Rooms are also destroyed

## Entity & Value Types

- Entity
-- An Object of Entity type has its own database identity (Primary Key)
- Value
-- An Object of Value type has no database identity (Primary Key). It belongs to an entity
-- Lifecycle of a Value type is bound to owning entity
-- Value type objects are identified through the owning entity

## JPA Persistence annotations

Annotation								|	Applied to	|	Description
----------------------------------------|---------------|--------------------------
@Entity									|	Class		|	Specifies that the class is an entity
@Table									|	Class		|	Specifies the primary table for the annotated entity. Additional tables may be specified using SecondaryTable or SecondaryTables annotation.
@Column									|	Field		|	Specifies the mapped column for a persistent property or field.
@Id										|	Field		|	Specifies the primary key of an entity.
@GeneratedValue							|	Field		|	<ul><li>Applied to a primary key property or field of an entity</li><li>AUTO: Hibernate selects the generation strategy based on the used dialect</li><li>IDENTITY: Hibernate relies on an auto-incremented database column to generate the primary key</li><li>SEQUENCE: Hibernate requests the primary key value from a database sequence</li><li>TABLE: Hibernate uses a database table to simulate a sequence</li></li><li>@GeneratedValue( strategy = GenerationType.IDENTITY )</li><li>@GeneratedValue( strategy = GenerationType.SEQUENCE, generator = "appUsersSeq" ) @SequenceGenerator( name = "appUsersSeq", sequenceName = "APP_USERS_SEQ", allocationSize = 1, initialValue = 1 )</li><li>@GeneratedValue( strategy = GenerationType.TABLE, generator = "appSeqStore" ) @TableGenerator( name = "appSeqStore", table = "APP_SEQ_STORE", pkColumnName = "APP_SEQ_NAME", pkColumnValue = "APP_USERS.APP_USERS_PK", valueColumnName = "APP_SEQ_VALUE", initialValue = 1, allocationSize = 1 )</li></ul>
@SequenceGenerator						|	Class/Field	|	Defines a primary key generator which will be referenced by @GeneratedValue
@OneToOne								|	Field		|	
@OneToMany								|	Field		|	
@ManyToOne								|	Field		|	
@ManyToMany								|	Field		|	
@Embeddable								|	Class		|	Specifies a class whose instances are stored as an intrinsic part of an owning entity and share the identity of the entity. Each of the persistent properties or fields of the embedded object is mapped to the database table for the entity.
@Embedded								|	Field		|	Specifies a persistent field or property of an entity whose value is an instance of an embeddable class. The embeddable class must be annotated as Embeddable.
@AttributeOverrides						|	Field		|	Used to override mappings of multiple properties or fields.
@AttributeOverride						|	Field		|	Applied to an embedded field or property to override the mapping defined by the embeddable class. If AttributeOverride is not specified, the column is mapped the same as in the original mapping.
@Access									|	Class		|	
@Transient								|	Field		|	Specifies that the property or field is not persistent
@Temporal								|	Field		|	<ul><li>Specified for persistent fields or properties of type java.util.Date and java.util.Calendar</li><li>TemporalType.DATE - Map as java.sql.Date</li><li>TemporalType.TIME - Map as java.sql.Time</li><li>TemporalType.TIMESTAMP - Map as java.sql.Timestamp</li></ul>
@Basic									|	Field		|	

## JPA Persistence enums

enum								|	Description
------------------------------------|--------------------------
@CascadeType						|	Defines the set of cascadable operations that are propagated to the associated entity. The value cascade=ALL is equivalent to cascade={PERSIST, MERGE, REMOVE, REFRESH, DETACH}.

