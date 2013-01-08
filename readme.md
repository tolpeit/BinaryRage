# BinaryRage - the ultra fast .NET document database
BinaryRage is designed to be a lightweight fast document database for .NET. 

No configuration, no server, no setup - simply reference the dll and start using it in less than a minute.

## Show me the code
Simple class - simple include [Serializable]
        [Serializable]
      	public class Product
      	{
          public string Title { get; set; }
      		public string ThumbUrl { get; set; }
      		public string Description { get; set; }
      		public float Price { get; set; }
      	}

Insert-syntax (same for create and update)
  BinaryRage.DB<List<Product>>.Insert("mykey", listOfProducts, @"C:\testpath");

Get the saved data
  var listOfProducts = BinaryRage.DB<List<Product>>.Get("mykey", @"C:\testpath");

That's it - can it be any simpler?


## Goals
Codebase and usage must be as simple as possible (but not simpler).

## Todo
- Better queue async writes of objects (must support rewriting the same object severel thousand times - where the last in queue wins and the rest is ignored)
- Include UnitTests

# FAQ
## Is it really fast?
We have tested more than 200,000 complex objects (documents) written to disk per second on a crappy laptop :-)

All writes are performed asynchronously.

## Why are you compressing the objects before written to disk?
The less I/O - the better. A compressed object is done less I/O because of less bytes written to disk.

## Why do I have to provide a path when I save an object?
I have decided that I want to provide sharding directly from the start. You can easily wrap the insert and get methods and "hardcode" the location if you want.
