# ADVA SOFT Code conventions

## 1. **namespace algotest** (all small letters with "_" if more than one word)
   It is recommended to store all classes in namespace retouch in "retouch" folder

## 2. **class RetouchAlgorithm** (Each word starts from a capital letter)
   .h and .cpp file name should correspond to the main class in the file (RetouchAlgorithm.h RetouchAlgorithm.cpp)
   .h file can contain several class definitions if they are auxiliary for the main class

## 3. **struct SomeStruct** (structures that can be copied field-by-field _MAY_ start from "T" letter)
   .h file should be named without prefix "SomeStruct.h"

## 4. **template<class T> SomeTemplateClass** (template classes can have prefix "T": template<class T> TException)
   .h file should be named without prefix "SomeTemplateClass.h"

## 5. **void getMoreInformation()** (class members. Java standard - first word starts from a small letter, all other - from a capital one)
	member name should be as informative as possible and not very long
	Is is recommended to have member names quite unique, so that search in project
	with the name refers to this member definition and use (CloneArray is better than Clone)


## 6. **int m_some_field** (class and struct fields names should start from "m_" ( all small letters )
   Exception: it is allowed to omit "m_" if a class is a common mathematical object like vector (x,y,z), quaternions, angles and so on

## 7. **const int KValue=5** constant values start from K
## 8. **_NOT ALLOWED_ #define KValue 5**

## 9. **enum EMyEnum { KValue1=0, KValue2=0 }** enum name starts from "E", field names - from "K"

## 10. **enum class EMyEnum { Value1=0, Value2=0 }** enum class name starts from "E", field names - from capital

## 11. **local variables i,j, some_variable** (lower case, _ separated)


# **---------------- Additionals -------------------**

## **1. Use treat warning-as-error compilation with level 4 warning. Code should be compiled without warnings.**

## **2. Do not use library if you are not sure it is available on iOs, MacOS, Windows and Android**

## **3. Always write comment if you are not sure that your code works fine and is easy to understand**

## **4. Do not write code that does not work and is not easy to understand**

## **5. Never write comment where code works fine and is easy to understand**

## **6. Write TODO comments**

     TODO comments must be up-to-date. There should be no obsolete or dummy TODO comments.

## **7. Always use the simplest way to code the concept. One concept is one member. Use STL containers.**

## **8. Use pointers with reference count only where code looks better with them**

    recommended to use "sysutils" (internal) library for pointers with reference counters
    check multithread-safety and support on iOs, MacOS, Windows and Android before using any other type of pointers with reference counters

## **9. Always use vertical brackets alignment. It is recommended to use TAB as indent symbol**

    Example 9.1 Proper bracket alignment
<pre>
    void f()
    {
        for(;;)
        {
            // code
        }
        switch(...)
        {
        case 1:
            //code
            break;
        default:
            //code
            break;
        }
    }
</pre>

<pre>
    class A
    {
    public:
        A() {}
    };
</pre>


## **10. Any function that is supposed not to change class members MUST BE const**

## **11. If class does not support field-by-field assign or initialization it**

    MUST DECLARE COPY CONSTRUCTOR AND PRIVATE ASSIGN OPERATOR as =delete
  Note 1. A(const A&)=delete; (not A(A&))
  Note 2. A& operator=(const A&)=delete; (not A& operator=(A&))

## **12. Always verify errors that are in system specification non-functional demand list**
  Example demand: THE SYSTEM BAHAVES PROPERLY ON MEMORY LACK
  Example 13 1 Memory allocation error handle on Win32
<pre>
  // Win 32
  char array[] = new char[10];
  if (!array) throw MemoryException();
</pre>

## **13. Never return error status if error is not supposed to be handled in a calling function**
    Example 14 1 Error or Exception
<pre>
    bool add_user_to_db(const CUser& user) throw(CommonException);
    {
        try
        {
            add(user);
        }
        catch(IndexDuplicationException&)
        {
            // user name check may be a part of calling function check
            return false;
        }
        // other exceptions (like no connection, no memory) are not part of normal execution
        return true;
    }

  // GOOD: exception
  void add_user_to_db(const CUser& user) throw(CDatabaseException);
</pre>

## **14. Write throw(Exc1, Exc1) specification only if you are 100% sure about all possible exceptions.**
 Otherwise program crashed on any exception not in a list

## **15. Interface is a preferred technique to hide implementation of big classes:**

<pre>
SomeClass.h
 class SomeClass
 {
 public:
	virtual ~SomeClass();
	virtual int someFunc()=0;
	static SomeClass ** createSomeClass();
 };


SomeClass.cpp
 class SomeClassImpl : public SomeClass
 {
	// a lot of members and fields
 public:
	virtual SomeClassImpl ();
	virtual int someFunc();
	
 };
 // ...
 SomeClass ** SomeClass::createSomeClass()
 {
 	return new SomeClassImpl();
 }
</pre>

## **16. NEVER STORE REFERENCES OR POINTERS TO FIELDS OF ANOTHER CLASS**

## **17. If some function returns pointer to an object, explain, how should it be released**
