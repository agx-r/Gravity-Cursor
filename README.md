# Gravity Cursor

This is a small C++ program that adds gravity to the mouse cursor on a Windows system. The program constantly updates the position of the cursor based on a gravity force and the current velocity vector.

## Prerequisites

- Windows operating system

## Usage

1. Clone the repository or download the source code file.
2. Open the source code file (`cursor.cpp`) in a C++ IDE or text editor.
3. Compile and run the program using a C++ compiler.
4. The program will add gravity to the mouse cursor, causing it to fall downwards.
5. Press `Ctrl+C` to exit the program.

## Code Explanation

The program uses the Windows API to interact with the operating system and manipulate the mouse cursor. Here is a brief explanation of the main parts of the code:

```cpp
const double GRAVITY = 1;   // Acceleration due to gravity

struct Vector2 {
    double x;
    double y;
};
```

- `GRAVITY`: Constant representing the acceleration due to gravity. You can adjust this value to change the strength of the gravity force.
- `Vector2`: A simple struct to store 2D vector coordinates (x and y).

```cpp
void moveCursorWithGravity()
{
    POINT p;			  // Stores the current mouse cursor position
    Vector2 velocity{};  // Stores the current velocity vector of the cursor
    Vector2 last_position{};
	
    while (true) {
        GetCursorPos(&p);  // Get the current mouse cursor position
				
        // Update velocity
        velocity.y += GRAVITY;
        
        if (p.y >= 1024)
        {
            velocity.y = 0;
            velocity.x = 0;
        }
		
        // Update cursor position with velocity
        SetCursorPos(p.x + velocity.x, p.y + velocity.y);
        
        Sleep(10);  // Sleep for a short interval to limit the cursor movement speed
        velocity.x = (velocity.x + (p.x - last_position.x)) / 2;
        velocity.y = (velocity.y + (p.y - last_position.y)) / 2;
        
        last_position.x = p.x;
        last_position.y = p.y;
    }
}
```

- `moveCursorWithGravity()`: Function that continuously updates the position of the mouse cursor with a gravity effect.
- `GetCursorPos(&p)`: Retrieves the current mouse cursor position and stores it in the `p` variable of type `POINT`.
- `velocity.y += GRAVITY`: Updates the velocity in the y-direction by adding the gravity constant.
- `if (p.y >= 1024)`: Checks if the cursor has reached the bottom of the screen (assuming a screen height of 1024 pixels). If so, resets the velocity to zero.
- `SetCursorPos(p.x + velocity.x, p.y + velocity.y)`: Updates the cursor position by adding the velocity components to the current position.
- `Sleep(10)`: Pauses the program execution for a short interval (10 milliseconds) to limit the cursor movement speed.
- `velocity.x = (velocity.x + (p.x - last_position.x)) / 2` and `velocity.y = (velocity.y + (p.y - last_position.y)) / 2`: Updates the velocity by averaging the difference between the current and last cursor positions.
- `last_position.x = p.x` and `last_position.y = p.y`: Updates the last cursor position for future velocity calculations.

```cpp
int main()
{
    std::cout << "Adding gravity to mouse cursor. Press Ctrl+C to exit." << std::endl;
    moveCursorWithGravity();
    return 

0;
}
```

- `main()`: The entry point of the program. Displays a message and calls the `moveCursorWithGravity()` function.

Feel free to modify and experiment with the code to customize the gravity effect or add additional functionality.

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

- This program was inspired by the concept of applying gravity to a mouse cursor.
