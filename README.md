#include <iostream>
using namespace std;

class Point {
public:
    double x, y;
    Point(double x, double y) : x(x), y(y) {}
};

class PhepBienDoi {
public:
    virtual void bienDoi(Point& p) = 0;
    void bienDoiMang(Point* arr, int size) {
        for (int i = 0; i < size; i++) {
            bienDoi(arr[i]);
        }
    }
};

class LatNgang : public PhepBienDoi {
private:
    double axis;
public:
    LatNgang(double axis) : axis(axis) {}
    void bienDoi(Point& p) override {
        p.x = 2 * axis - p.x;
    }
};

class LatDoc : public PhepBienDoi {
private:
    double axis;
public:
    LatDoc(double axis) : axis(axis) {}
    void bienDoi(Point& p) override {
        p.y = 2 * axis - p.y;
    }
};

class PhepDich : public PhepBienDoi {
private:
    double shift_x, shift_y;
public:
    PhepDich(double shift_x, double shift_y) : shift_x(shift_x), shift_y(shift_y) {}
    void bienDoi(Point& p) override {
        p.x += shift_x;
        p.y += shift_y;
    }
};

int main() {
    Point P[3] = { Point(1, 2), Point(3, 4), Point(5, 6) };

    PhepBienDoi* A[10];
    A[0] = new LatNgang(10.0);
    A[1] = new LatDoc(5.0);
    A[2] = new PhepDich(2.0, 3.0);

    for (int i = 0; i < 3; i++) {
        cout << "Toa do ban dau: (" << P[i].x << ", " << P[i].y << ")" << endl;
        for (int j = 0; j < 3; j++) {
            A[j]->bienDoi(P[i]);
            cout << "Bien doi " << j+1 << ": (" << P[i].x << ", " << P[i].y << ")" << endl;
        }
        cout << endl;
    }

    for (int i = 0; i < 3; i++) {
        delete A[i];
    }

    return 0;
}

