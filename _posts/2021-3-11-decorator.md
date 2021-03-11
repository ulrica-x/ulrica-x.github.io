.h
#include <iostream>

class Shape {
public:
    virtual ~Shape() {}
    virtual void draw() = 0;
};

class Triangle : public Shape {
public:
    void draw() override {
        std::cout << "Triangle" << std::endl;
    }
};

class Round : public Shape {
public:
    void draw() override {
        std::cout << "Round" << std::endl;
    }
};

class ShapeDecorator : public Shape {
public:
    ShapeDecorator(Shape * decorated_shape) : m_decorated_shape(decorated_shape) {}
    ~ShapeDecorator() {}
protected:
    Shape *m_decorated_shape;
};

class ShapeDecoratorColorRed : public ShapeDecorator {
public:
    ShapeDecoratorColorRed(Shape * decorated_shape) : ShapeDecorator(decorated_shape) {}
    void draw() {
        std::cout << "Red ";
        m_decorated_shape->draw();
    }
};

class ShapeDecoratorColorBlue : public ShapeDecorator {
public:
    ShapeDecoratorColorBlue(Shape * decorated_shape) : ShapeDecorator(decorated_shape) {}
    void draw() {
        std::cout << "Blue ";
        m_decorated_shape->draw();
    }
};

class ShapeDecoratorColorSentimental : public ShapeDecorator {
public:
    ShapeDecoratorColorSentimental(Shape * decorated_shape) : ShapeDecorator(decorated_shape) {}
    void draw() {
        std::cout << "Sentimental ";
        m_decorated_shape->draw();
    }
};


.cpp
#include "decorator_demo.h"

int main() {
    Triangle triangle;
    Round round;

    ShapeDecoratorColorBlue blue(&triangle);
    blue.draw();

    ShapeDecoratorColorRed red(&triangle);
    red.draw();

    ShapeDecoratorColorBlue blue1(&round);
    blue1.draw();

    ShapeDecoratorColorRed red1(&round);
    red1.draw();

    ShapeDecoratorColorSentimental sentimental(&blue);
    sentimental.draw();

    return 0;
}
