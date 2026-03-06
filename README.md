# STM32 Dino Game

A Chrome Dino-style endless runner game for STM32F401RE microcontroller with ST7735 TFT display.

## Hardware Requirements

- **Microcontroller**: STM32F401RE (NUCLEO-F401RE board)
- **Display**: ST7735 128x160 TFT LCD
- **Touch Sensor**: Connected to PC8 (active HIGH)

## Pin Configuration

| Function | Pin | Description |
|----------|-----|-------------|
| SPI SCK  | PA5 | SPI Clock |
| SPI MOSI | PA7 | SPI Data Out |
| TFT RST  | PC7 | Display Reset |
| TFT CS   | PB6 | Chip Select |
| TFT DC   | PA9 | Data/Command |
| TOUCH    | PC8 | Touch Sensor Input |

## Features

- Black background with white character theme
- Smooth 60 FPS gameplay at 84 MHz
- Touch-based jump control
- Progressive difficulty (speed increases with score)
- High score tracking
- Animated dinosaur sprite
- Random obstacle generation (small and large cacti)
- Scrolling ground and clouds

## Performance Optimizations

1. **Clock Speed**: STM32F401 running at 84 MHz (PLL configured)
2. **SPI Speed**: 10.5 MHz (prescaler /8) for fast display updates
3. **Batch Transfers**: 256-byte buffer for efficient pixel rendering
4. **Optimized Drawing**: Single HAL call per scanline for sprites

## Game Controls

- **Touch PC8**: Jump (when on ground)
- **Auto-restart**: Touch to restart after game over

## Building the Project

### Using STM32CubeIDE

1. Open STM32CubeIDE
2. Import this project: `File > Open Projects from File System`
3. Build the project: `Project > Build All`
4. Flash to board: `Run > Debug` or `Run > Run`

### Using Command Line

```bash
cd Debug
make clean
make all
```

### Flashing with STM32CubeProgrammer

```bash
STM32_Programmer_CLI -c port=SWD -w Debug/snake.elf -v -rst
```

## Game Mechanics

- **Jump Physics**: Fixed-point arithmetic (1/4 pixel precision)
- **Initial Jump Velocity**: -38 (fixed-point)
- **Gravity**: 3 (fixed-point)
- **Initial Speed**: 8 (fixed-point)
- **Max Speed**: 28 (fixed-point)
- **Speed Increase**: Every 80 points

## Color Scheme

- Background: Black (0x0000)
- Dinosaur: White (0xFFFF)
- Obstacles: White (0xFFFF)
- Ground: Gray (0x8410)
- Score: Gray (0x8410)
- Sky Pattern: Light Gray (0xC618)
- Clouds: Light Gray (0xDEFB)
- Flash (Game Over): Red (0xF800)

## Project Structure

```
├── Core/
│   ├── Inc/          # Header files
│   ├── Src/          # Source files (main.c contains game logic)
│   └── Startup/      # Startup assembly
├── Drivers/          # STM32 HAL drivers
├── Debug/            # Build output
└── README.md
```

## License

This project uses STM32 HAL drivers which are licensed under BSD-3-Clause.

## Author

Dhanush G Kulal

## Repository

https://github.com/Dhanushgkulal/Dino_game
