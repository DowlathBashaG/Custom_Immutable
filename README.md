# Custom_Immutable

	- Make your class final
	- Declare all instance variable with private and final
	- Say no to setter methods. (only setter methods)
	- Initialize all the variables in constructor
	- You can initialize variable in constructor
	- Perform cloning of mutable objects while returning from getter method

Important Points :
------------------

	- Do the clone if it is object . Example Date doj.....it is object need to clone like this : (Date)doj.clone();
	- Return the object. like this -> return new ArrayList<>(mobile); return new Address(address.getCity().address.getZip());


Example :
-------

Employee.java :

	public final class Employee{
	
	private final String name;
	private final Data doj;  //mutable
	private final List<String> mobile;
	
	private final Address address;  // mutable ...need to make forcefully immutable

// usecase : 3 

	// we have address class, this class is completly mutable class.with setter and getter methods


	public Employee(String name,Date doj, List<String> mobile, Address address){
	this.name = namel
	this.doj = doj;
	this.mobile = mobile;
	this.address = address;
	}

	public String getName(){
	//return doj;  // To avoid this issue , rather than direct returning object. Instead of this , clone it.
	return (Date)doj.clone(); // after this it is not allowed to set new date.
	}

	public List<String> getMobile(){
	//return mobile;
	//return Collections.unmodifiableList(mobile); // it is throwing exception when we try to add new value into list.[ UnsupportedOperationException ] we dont need //to give any exception.our moto is use should not add numbers in to the list.
	return new ArrayList<>(mobile); // this is correct approach. Now it wont allow and not throwing exception also.
	
	}

	public Address getAddress(){
	//return address; // instead of this make a separate copy of this address like new Address(address.getCity().address.getZip()); in that case it wont change it.
	return new Address(address.getCity(),address.getZip()); // it will work.
	}

	@Override
	public String toString(){
	return "Employee{"+ "name= '"+name+'\''+",doj ="+doj+",mobile="+mobile+",address= "+ address + 
	'}';

	public static void main(String args[]{
	Address address = new Address("Bangalore","1011");
	Employee employee = new Employee("Dowlath",new Date(),
	                    Arrays.stream(new String[]{"1234","5678"})
						.collect(Collectors.toList()),address);

	//employee.name ="Basha";// it is crying...compile time error. so comment now. It is fulfilling the immuatble rule. Not able to update.	

// Use case : 1

	// We are able to modify doj or not.	
	employee.getDoj().setDate(10);  <---should not print the date 10. It is updating the date. immutable means should not update or change the date.
	// for this direct returning , instead of this , clone it.


// Use case : 2

 	// We are able to modify the list or not.
	employee.getMobile().add("9000"); // it is allowing to update the list.It should not allow.


// Use case : 3 

	// Should not able to modify Bangalore to Pune. it should not allow.
	employee.getAddress().setCity("Pune");   // Now city is changed how we can resolved , instead of return address , make a separate copy of it.
	
	System.out.println(employee);
	}
	}
 
Use case : 3

We have address class.
	
	public class Address{
	private String city;
	private String zip;
	
	public 	Address(){
	}
	
	public Address(String city,String zip){
	  this.city = city;
	  this.zip = zip;
	}
	
	public String getCity(){
	return city;
	}
	
	public void setCity(String city){
	this.city = city;
	}
	
	public String getZip(){
	return zip;
	}
	
	public void setZip(String zip){
	this.zip = zip;
	}
	
	// toString method here
	
	}	
