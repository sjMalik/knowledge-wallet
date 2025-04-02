```js
if (bird.active) {
    // Apply gravity-like effect when no input is given
    bird.setVelocityY(bird.body.velocity.y + 10);
    let baseTop = game.config.height - base.height;
    if (bird.y + bird.height / 2 > baseTop) {
        bird.y = baseTop - bird.height / 2;
        bird.setVelocityY(0); // Stop bird movement when it hits the ground
    }
}
```

### Gravity Simulation

This code snippet simulates a gravity-like effect for the bird sprite in a Phaser 3 game and ensures that the bird does not fall below the base of the game scene. It also handles the bird's interaction with the ground, stopping its movement when it reaches the base.

#### Key Features

1. **Gravity Effect**  
   The condition `if (bird.active)` ensures that the logic is only applied when the bird is active in the game. This prevents unnecessary calculations or updates when the bird is not in play (e.g., during a game-over state or before the game starts).  
   The line `bird.setVelocityY(bird.body.velocity.y + 10)` increases the bird's vertical velocity by 10 units on each frame, simulating the effect of gravity pulling the bird downward. The value `10` represents the strength of the gravity effect and can be adjusted to make the bird fall faster or slower, depending on the desired gameplay mechanics.

2. **Preventing the Bird from Falling Below the Base**  
   - The variable `baseTop` calculates the vertical position of the top edge of the base using `game.config.height - base.height`. This value represents the boundary where the bird should stop falling.  
   - The `if` condition checks whether the bottom edge of the bird (`bird.y + bird.height / 2`) has moved below the top of the base (`baseTop`). If this condition is true, the bird's position is corrected by setting its `y` coordinate to `baseTop - bird.height / 2`. This adjustment ensures that the bird's bottom edge aligns perfectly with the top of the base, preventing it from visually overlapping or falling through the ground.  
   - Additionally, the line `bird.setVelocityY(0)` stops the bird's vertical movement when it hits the ground. This ensures that the bird remains stationary on the base until further input is provided.

### Summary

This code creates a realistic gravity effect for the bird while enforcing a boundary to keep it above the base. It ensures smooth gameplay by stopping the bird's movement when it reaches the ground, preventing unintended behavior such as falling through the base. This logic is essential for games where objects interact with a ground or platform, such as side-scrolling or endless runner games.