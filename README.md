# SFAS

SFAS (SFML Assets) is something I've been working on for a couple months that adds cool widgets and stuff to your SFML project.

I've written basicly ZERO documentation for this so..... ;-;

Anyone is welcome to steal this code (with credit though) and use and change however you like, if you can manage to figure out how it works.

This was build using SFML 3.0.0 snapshot.

Here's what my default setup code usally looks like,:

```
#include <iostream>

//Includes all the main widgets
#include "SFAS/Widgets.hpp"
//This will find the path to the exe/app on both windows and mac automaticly, SUPER usefull
#include "SFAS/RpFinder.hpp"
//This helps with converting two numbers (or 1) or a sf::Vector<int> to a sf::Vector<float>
// this is what all the c(x, y) is
#include "SFAS/Conversion.hpp"

using sfas::c;
using sfas::rp;

int main()
{
    //Creating the window
    sf::RenderWindow window(sf::VideoMode(sf::Vector2u(800, 800)), "SFML assets", (sf::Style::Titlebar | sf::Style::Close));
    
    // Making the widget manger, this will mage all your widgets, although you still need to store them.
    sfas::WidgetManager widgetManager;
    // This allows all widgits to load and use the same font
    sfas::Widget::setFont(rp() + "sansation.ttf");
    
    // Creating a button and then regestering it with the widget manager, firct group of numbers is position, second is size
    sfas::Button button(c(350, 350), c(100, 100));
    button.setColor(sf::Color::Red);
    widgetManager.registerWidget(&button);
    
    while (window.isOpen()) {
        sf::Event event;
        
        while (window.pollEvent(event)) {
            // Every event gets passed to the widget manager which in turn passes it to each widget
            widgetManager.checkEventForStack(event);
            if(event.type == sf::Event::Closed)
                window.close();
        }
        // Ticks every registered widget
        widgetManager.tickStack(window);
        
        
        if(button.clickedOnTick){
          std::cout << "Click\n";
          }
        
        
        window.clear();
        // Renders all the widgets
        widgetManager.renderStack(window);
        window.display();
    }
    
}

```

Most widgets can have textures.

The ones I use most is the button and the canvas, the canvas widgewt is alot like the HTML canvas.
