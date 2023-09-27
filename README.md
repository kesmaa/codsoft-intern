# codsoft-intern
I am uploading my codsoft internships task in this repository. I hava tried to incorporate every possible feature in my projects. If you have any query related to my work, feel free to contact me.
#include <iostream>
#include <vector>
#include <iomanip>

using namespace std;

// Define a Movie class to represent movies
class Movie {
public:
    string title;
    string genre;
    int duration;

    Movie(const string& title, const string& genre, int duration)
        : title(title), genre(genre), duration(duration) {}
};

// Define a Seat class to represent individual seats in the theater
class Seat {
public:
    int seatNumber;
    bool isBooked;

    Seat(int seatNumber) : seatNumber(seatNumber), isBooked(false) {}
};

// Define a Booking class to represent a booking
class Booking {
public:
    string movieTitle;
    int seatNumber;

    Booking(const string& movieTitle, int seatNumber)
        : movieTitle(movieTitle), seatNumber(seatNumber) {}
};

// Define a Theater class to manage movies and seats
class Theater {
public:
    vector<Movie> movies;
    vector<Seat> seats;
    vector<Booking> bookings;

    void addMovie(const Movie& movie) {
        movies.push_back(movie);
    }

    void displayMovies() {
        cout << "Movies playing at the theater:" << endl;
        for (const Movie& movie : movies) {
            cout << "Title: " << movie.title << " | Genre: " << movie.genre
                 << " | Duration: " << movie.duration << " minutes" << endl;
        }
    }

    void displaySeats() {
        cout << "Available seats:" << endl;
        for (const Seat& seat : seats) {
            if (!seat.isBooked) {
                cout << "Seat " << seat.seatNumber << " ";
            }
        }
        cout << endl;
    }

    bool bookSeat(const string& movieTitle, int seatNumber) {
        for (Seat& seat : seats) {
            if (seat.seatNumber == seatNumber && !seat.isBooked) {
                seat.isBooked = true;
                bookings.push_back(Booking(movieTitle, seatNumber));
                return true;
            }
        }
        return false;
    }
};

int main() {
    Theater theater;

    // Add some movies to the theater
    theater.addMovie(Movie("Avengers: Endgame", "Action", 181));
    theater.addMovie(Movie("Joker", "Drama", 122));
    theater.addMovie(Movie("Toy Story 4", "Animation", 100));

    // Initialize seats
    for (int i = 1; i <= 10; ++i) {
        theater.seats.push_back(Seat(i));
    }

    char choice;
    do {
        cout << "1. Display Movies\n2. Book a Seat\n3. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case '1':
                theater.displayMovies();
                break;
            case '2':
                theater.displayMovies();
                string movieTitle;
                int seatNumber;
                cout << "Enter the movie title: ";
                cin.ignore();
                getline(cin, movieTitle);
                cout << "Enter the seat number: ";
                cin >> seatNumber;
                if (theater.bookSeat(movieTitle, seatNumber)) {
                    cout << "Seat booked successfully!" << endl;
                } else {
                    cout << "Seat not available or invalid seat number." << endl;
                }
                break;
            case '3':
                cout << "Thank you for using our ticket booking system. Goodbye!" << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
                break;
        }
    } while (choice != '3');

    return 0;
}
