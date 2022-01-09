# ConvertingKotlin

A Google CodeLab

## personal notes

### general

no visibility modifier is public by default

### classes

default values may be defined as: e.g. 

data class User(var firstName: String?, var lastName: String?)
* User user = User("John", "Doe")
* User user = User("John") // lastName == null
* User user = User(lastName = "Doe") // firstName == null

data : declares an object that only contains data (similar to POJO); derives equals(), hashCode() and toString()

fun : declares a function; like 'class' declares a class

object : replaces 'class' keyword in declaration to enforce singleton property

primary ctor cannot contain any initialization code
* any initialization code is migrated to an 'init' block

all static fields and functions are migrated to a 'companion object' block

singletons are converted to private ctor with companion object
* remove private ctor and companion object by replacing 'class' keyword with 'object'

get/set not considered as funcs so converted to field/prop with internal accessor

where replacing get func with prop, can expose immutable for internal mutable 
* e.g. backing property
* change fun getObjects(): List<Object>? { return objects} to:
* private val _objects = mutableListOf<Objects>()
*   val objects: List<Objects>	
*     get() = _objects

extension functions/properties can be declared outside class for use in other contexts
* as compared with static util methods/constants in java

scope functions (let|apply|with|run|also) can be added to funcs/props
* execute code in context of object (e.g. Repository) without explicity naming object
* e.g. objects is prop, call objects.apply to execute corresponding code block

### instances

val : declares an immutable (i.e. constant) instance; like 'final' in Java

var : declares a mutable instance

typed objects may remove the type definition by including type in assigned instance

e.g. 
* val objectIds : MutableArrayList<Object> = ArrayList(objects.size)
* val objectIds = ArrayList<Object>(objects.size)

### nullability

var not instantiated at declaration 
* is declared as nullable
* all uses/instances are asserted as non-null with !! 
* throws runtimeex if assigned value is null
* instead use nullcheck (if users!= null) {}, elvis op (?:) or using kotlin std fun
* uninitialized list declared as nullable can be initialized with mutableListOf<T?>()
* mutableListOf() creates immutable empty list (mutable contents)

### conditionals

'for each' syntax is (object in objects) instead of for(Object object : objects)

destructuring allows for declaration of multiple fields of data class instance

e.g. ((field 1, field 2, ...) in objects)

if, for and while expressions can be assigned because the last line returns a value

elvis operator between two exps returns first exp if nonull, otherwise second exp

map function moves loop logic inside map item body reducing need for iteration

### formatting

place $ before instance val ref between quotes, not concat instance val ref w/ str

e.g.
 
* do "$field1 $field2 ..." or "${object.field1} ${object.field2} ..." 

& not field1 + " " + field2

