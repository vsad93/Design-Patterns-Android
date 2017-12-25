package com.example.ari.designpatterns;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

import com.example.ari.designpatterns.AbstractFactory.AbstractFactory;
import com.example.ari.designpatterns.AbstractFactory.Color;
import com.example.ari.designpatterns.AbstractFactory.FactoryProducer;
import com.example.ari.designpatterns.AbstractFactory.Shape;
import com.example.ari.designpatterns.Builder.Person;
import com.example.ari.designpatterns.FactoryAndNullObjectPattern.Car;
import com.example.ari.designpatterns.FactoryAndNullObjectPattern.CarFactory;
import com.example.ari.designpatterns.Prototype.School;

import java.sql.SQLException;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

    }

    public void builderExample() {

        /*
        CREATES A NEW PERSON OBJECT FROM PERSONBUILDER CLASS.
        SINCE EACH OF THE SET METHODS RETURNS A PERSONBUILDER, WE NEED TO CONCLUDE
        THE METHOD CALL CHAIN WITH A .BUILD CALL, WHICH RETURNS A NEW PERSON OBJECT,
        THAT TAKES IN THE PERSONBUILDER AS A PARAMETER.
         */
        Person person = new Person.PersonBuilder()
                .firstName("John")
                .lastName("Smith")
                .motherName("Carry")
                .fatherName("Jim")
                .address("612 Main St")
                .city("Queens")
                .state("NY")
                .build();


    }

    public void prototypeExample() {
                /*
        HERE WE SEE A PRACTICAL USE OF THE PROTOTYPE DESIGN PATTERN.
        IT IS PRIMARILY USED IF WE ARE LOOKING TO CLONE AN ITEM STORED
        IN THE PHONE. INSTEAD OF PULLING UP THE SAME RECORD FROM STORAGE TWICE,
        WHICH CAN TAKE TIME, WE PERFORM A DEEP COPY OF THE FIRST ITEM.

        ADDITIONALLY, IN THE LOADSCHOOL METHOD, YOU WILL SEE THE SINGLETON DESIGN  PATTERN
        AND DAO DESIGN PATTERN AT WORK (IN THE DATAHELPER CLASS)
         */
        School school = new School();
        school.setSchoolName("School 1");
        try {
            school = new School().loadSchool(1);
        } catch (SQLException e) {
            e.printStackTrace();
        }

        try {
            School school1 = school.clone();
            school1.setSchoolName("school 2");
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }

    public void factoryExample() {
        CarFactory factory = new CarFactory();
        Car car = factory.getInstance("SUV");
        car.speak();

    }

    public void abstractPattern() {

        //get shape factory
        AbstractFactory shapeFactory = FactoryProducer.getFactory("SHAPE");

        //get color factory
        AbstractFactory colorFactory = FactoryProducer.getFactory("COLOR");
        //get an object of Shape Circle
        assert shapeFactory != null;
        Shape shape1 = shapeFactory.getShape("CIRCLE");

        //call draw method of Shape Circle
        shape1.draw();

        //get an object of Shape Rectangle
        Shape shape2 = shapeFactory.getShape("RECTANGLE");

        //call draw method of Shape Rectangle
        shape2.draw();

        //get an object of Shape Square
        Shape shape3 = shapeFactory.getShape("SQUARE");

        //call draw method of Shape Square
        shape3.draw();


        //get an object of Color Red
        assert colorFactory != null;
        Color color1 = colorFactory.getColor("RED");

        //call fill method of Red
        color1.fill();

        //get an object of Color Green
        Color color2 = colorFactory.getColor("Green");

        //call fill method of Green
        color2.fill();

        //get an object of Color Blue
        Color color3 = colorFactory.getColor("BLUE");

        //call fill method of Color Blue
        color3.fill();

    }
}
