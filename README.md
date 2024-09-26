# Creacional/Comercio/Creacion de objetos

## Ruleta 1
### Categoria creacional: Factory Method

## Ruleta 2
### Dominio Comercio electronico

## Ruleta 3
### Requisito Necesidad de flexibilidad en la creacion de objetos

## Codigo
```
using System;

// Definimos una interfaz que todos los usuarios deben implementar
public interface IUser
{
    void GetUserType();
}

// Clase concreta para el cliente
public class Customer : IUser
{
    public void GetUserType()
    {
        Console.WriteLine("Soy un Cliente.");
    }
}

// Clase concreta para el vendedor
public class Seller : IUser
{
    public void GetUserType()
    {
        Console.WriteLine("Soy un Vendedor.");
    }
}

// Clase Factory: aquí definimos el método que crea objetos dependiendo del tipo de usuario
public abstract class UserFactory
{
    public abstract IUser CreateUser();
}

// Factory concreta para crear un Cliente
public class CustomerFactory : UserFactory
{
    public override IUser CreateUser()
    {
        return new Customer();
    }
}

// Factory concreta para crear un Vendedor
public class SellerFactory : UserFactory
{
    public override IUser CreateUser()
    {
        return new Seller();
    }
}

// Programa principal
public class Program
{
    public static void Main(string[] args)
    {
        // Creamos una instancia de la fábrica dependiendo del tipo de usuario
        UserFactory userFactory;
        
        Console.WriteLine("Ingrese el tipo de usuario (cliente o vendedor): ");
        string userType = Console.ReadLine();

        if (userType.ToLower() == "cliente")
        {
            userFactory = new CustomerFactory();
        }
        else if (userType.ToLower() == "vendedor")
        {
            userFactory = new SellerFactory();
        }
        else
        {
            Console.WriteLine("Tipo de usuario no válido.");
            return;
        }

        // Usamos la fábrica para crear el usuario
        IUser user = userFactory.CreateUser();
        user.GetUserType();
    }
}

```
https://dotnetfiddle.net/wFAJcR

El código implementa el patrón Factory Method para un sistema de comercio electrónico, en el cual se puede crear dinámicamente un objeto Customer (cliente) o Seller (vendedor) según la entrada del usuario. Utiliza fábricas concretas (CustomerFactory y SellerFactory) que generan instancias específicas de cada tipo de usuario, cumpliendo con la interfaz común IUser. Dependiendo de si el usuario ingresa "cliente" o "vendedor", el programa instanciará el tipo correspondiente y mostrará un mensaje indicando el tipo de usuario creado, proporcionando flexibilidad en la creación de objetos según el contexto.
