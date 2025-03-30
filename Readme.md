# Phaser 3 Game Project

```javascript
import Phaser from "phaser";
// Phaser 3 game configuration object with type, width, height, physics, and scene properties
const config = {
  type: Phaser.AUTO,
  width: 800,
  height: 600,
  scene: {
    preload,
    create,
    update
  }
};
```

This code snippet is part of a Phaser 3 game project, which is a popular JavaScript framework for creating 2D games. The first line imports the Phaser library, making its functionality available for use in this file. This is possible because the project is using a module-based system, likely managed by a tool like npm.

The config object defines the core configuration for the Phaser game. It specifies several key properties that determine how the game will behave and render:

- **type: Phaser.AUTO**: This property tells Phaser to automatically choose the best rendering method available. It will prioritize WebGL for better performance and fallback to Canvas if WebGL is not supported by the user's browser.

- **width: 800 and height: 600**: These properties define the resolution of the game canvas in pixels. The game will have a width of 800 pixels and a height of 600 pixels, which determines the visible area of the game.

- **scene**: This property is an object that specifies the lifecycle methods for the game scene. It includes:
  - **preload**: A function where assets (e.g., images, sounds) are loaded before the game starts.
  - **create**: A function where the game world is initialized, such as adding sprites and setting up the scene.
  - **update**: A function that is called repeatedly (typically 60 times per second) to handle game logic, animations, and interactions.

This config object will be passed to the `Phaser.Game` constructor to initialize the game. It serves as the foundation for setting up the game's rendering, dimensions, and scene lifecycle, ensuring that the game behaves as intended.

---

```javascript
function create() {
  background = this.add.tileSprite(0, 0, game.config.width, game.config.height, "background");
  background.setScale(3);
  // Add the bird sprite to the scene
  bird = this.add.sprite(game.config.width / 2, game.config.height / 2, 'bird1'); // Position the bird in the middle of the game bounds
  bird.setScale(1); // Scale the bird down if needed
}
```

The `create` function in this code snippet is part of the Phaser 3 game framework and is responsible for setting up the game scene after assets have been preloaded. It initializes two key elements: the background and a bird sprite.

- The first line adds a background to the scene using `this.add.tileSprite`. A `tileSprite` is a special type of sprite that can repeat itself seamlessly, which is useful for creating scrolling or tiled backgrounds. The parameters `(0, 0)` position the background at the top-left corner of the game canvas, while `game.config.width` and `game.config.height` set its width and height to match the game's dimensions. The `"background"` string refers to the key of the preloaded background image. The `setScale(3)` method scales the background by a factor of 3, effectively enlarging it. This is useful if the original image is smaller than the game canvas or if a zoomed-in effect is desired.

- Next, the code adds a bird sprite to the scene using `this.add.sprite`. The bird is positioned at the center of the game canvas, with its x-coordinate set to `game.config.width / 2` and its y-coordinate set to `game.config.height / 2`. The `'bird1'` string refers to the key of the preloaded bird image. The `setScale(1)` method is called on the bird sprite, which keeps its size unchanged. This method can be adjusted to scale the bird up or down if needed, depending on the desired visual effect.

In summary, this `create` function sets up a visually scaled background and positions a bird sprite at the center of the game canvas. These elements form the foundation of the game scene, and additional logic or interactivity can be added in subsequent steps.

---

```javascript
function update() {
  // Move the background horizontally to create a scrolling effect
  background.tilePositionX += 0.5; // Adjust the speed as needed
  // Make the bird fly up and down
  bird.y += birdDirection * 1; // Adjust the speed of movement
  if (bird.y <= 250 || bird.y >= 350) {
    birdDirection *= -1; // Reverse direction when reaching bounds
  }
  // Animate the bird by cycling through frames
  birdFrame += 0.1; // Adjust the speed of animation
  if (birdFrame >= birdFrames.length) {
    birdFrame = 0; // Reset to the first frame
  }
  bird.setTexture(birdFrames[Math.floor(birdFrame)]);
}
```

The `update` function in this code snippet is part of the Phaser 3 game framework and is called repeatedly, typically 60 times per second, as part of the game loop. It handles the dynamic behavior of the game elements, including background scrolling, bird movement, and bird animation.

- The first section of the function creates a scrolling background effect by modifying the `tilePositionX` property of the `background` object. By incrementing this property by `0.5` on each frame, the background appears to move horizontally, simulating motion. The speed of the scrolling effect can be adjusted by changing the increment value.

- The second section controls the vertical movement of the bird sprite. The bird's `y` position is updated by adding `birdDirection * 1` to it, where `birdDirection` determines the direction of movement (`1` for downward, `-1` for upward). If the bird's `y` position reaches the bounds of `250` or `350`, the `birdDirection` is reversed by multiplying it by `-1`. This creates an oscillating effect, making the bird move up and down between the specified bounds. The speed of this movement can be adjusted by modifying the multiplier (currently `1`).

- The final section animates the bird by cycling through its frames. The `birdFrame` variable, which tracks the current frame, is incremented by `0.1` on each frame. If `birdFrame` exceeds the number of available frames (`birdFrames.length`), it is reset to `0`, ensuring the animation loops continuously. The `Math.floor` function is used to round `birdFrame` to the nearest integer, and the `setTexture` method updates the bird's texture to the corresponding frame from the `birdFrames` array. The speed of the animation can be adjusted by changing the increment value for `birdFrame`.

In summary, this `update` function brings the game to life by creating a scrolling background, making the bird move up and down, and animating the bird's appearance. These dynamic behaviors enhance the visual appeal and interactivity of the game.

```bash
npm create vite@latest
```

This command initializes a new project using Vite, a fast and modern build tool for web applications. The @latest ensures that the most recent version of Vite is used. When you run this command, it will prompt you to provide details about your project, such as the project name, framework (e.g., React, Vue, or vanilla JavaScript), and other configuration options. Vite is known for its fast development server and optimized build process, making it a popular choice for modern web development.

```bash
npm install phaser
```

```js
physics: {
    default: 'arcade',
    arcade: {
      gravity: { y: 0 },
      debug: false
    }
  }
```

```markdown
This code snippet defines the physics configuration for a Phaser 3 game. The `physics` property is part of the game's configuration object and specifies how the physics system should behave. Phaser supports multiple physics engines, and this configuration uses the built-in Arcade Physics engine, which is lightweight and suitable for 2D games.

- **`default: 'arcade'`**: This sets the default physics engine for the game to "arcade." The Arcade Physics engine is simple and efficient, making it ideal for games that require basic collision detection and physics simulations.

- **`arcade: {}`**: This nested object contains specific settings for the Arcade Physics engine:
  - **`gravity: { y: 0 }`**: This sets the global gravity for the game. The `y: 0` value means there is no vertical gravity, so objects will not fall automatically. This is useful for games where gravity is not a factor, such as top-down or side-scrolling games where movement is controlled manually.
  - **`debug: false`**: This disables the debug mode for the physics engine. When `debug` is set to `true`, Phaser will visually display collision boundaries and other physics-related information, which is helpful during development for troubleshooting. Setting it to `false` ensures that these visual aids are not shown in the final game.

In summary, this configuration initializes the Arcade Physics engine with no gravity and disables debug visuals. This setup is well-suited for games where objects need to move freely without being affected by gravity, and where a clean visual presentation is desired during gameplay.

---

```javascript
let baseImage = this.textures.get("base");
let baseHeight = baseImage.getSourceImage().height;
base = this.add.tileSprite(
  game.config.width / 2,
  game.config.height - baseHeight / 2,
  game.config.width,
  baseHeight,
  "base"
);
this.physics.add.existing(base, true);
base.setDepth(1);
```

This code snippet is part of a Phaser 3 game and is responsible for adding a "base" element to the game scene. The base is likely a static platform or ground element that serves as part of the game's environment.

- **`this.textures.get("base")`**: This retrieves the texture associated with the key `"base"` from the game's texture manager. The texture manager is responsible for managing all loaded assets, such as images and sprites.

- **`baseImage.getSourceImage().height`**: This accesses the source image of the `"base"` texture and retrieves its height. This value is used to calculate the vertical position of the base within the game scene.

- **`this.add.tileSprite(...)`**: This creates a tiled sprite for the base. A tiled sprite is an image that can repeat itself seamlessly, which is useful for creating elements like platforms or scrolling backgrounds. The parameters specify:
  - `game.config.width / 2`: The x-coordinate, positioning the base horizontally at the center of the game canvas.
  - `game.config.height - baseHeight / 2`: The y-coordinate, positioning the base vertically near the bottom of the canvas, with its center aligned to the calculated position.
  - `game.config.width`: The width of the base, matching the width of the game canvas.
  - `baseHeight`: The height of the base, derived from the source image.
  - `"base"`: The key for the texture to use for the tiled sprite.

- **`this.physics.add.existing(base, true)`**: This adds the base to the physics system as a static body. The second parameter, `true`, indicates that the base is immovable, meaning it will not respond to forces or collisions but can interact with other physics-enabled objects.

- **`base.setDepth(1)`**: This sets the rendering depth of the base. Depth determines the draw order of game objects, with higher values being rendered on top of lower values. By setting the depth to `1`, the base is ensured to appear above objects with a lower depth.

In summary, this code creates a static, physics-enabled base element that spans the width of the game canvas and is positioned near the bottom. It uses the `"base"` texture and ensures the base is rendered at the appropriate depth in the scene. This setup is typical for games that require a ground or platform for other objects to interact with.

---

```javascript
// Function to create a random-sized piller
const createPiller = () => {
  let pillerHeight = Phaser.Math.Between(100, 300); // Random height between 100 and 300
  let piller = this.add.sprite(
    game.config.width,
    game.config.height - base.height,
    "piller"
  );
  piller.displayHeight = pillerHeight; // Adjust the height of the piller
  piller.setOrigin(0.5, 1); // Set origin to the bottom center
  this.physics.add.existing(piller);
  piller.body.setVelocityX(-100); // Move the piller to the left

  // Remove the piller when it goes out of bounds
  piller.body.onWorldBounds = true;
  piller.body.world.on("worldbounds", (body) => {
    if (body.gameObject === piller) {
      piller.destroy();
    }
  });
};

// Create a new piller every 2 seconds
this.time.addEvent({
  delay: 2000,
  callback: createPiller,
  loop: true,
});
```

This code snippet defines a function, `createPiller`, which dynamically generates "piller" (pillar) objects in a Phaser 3 game. These pillars are likely obstacles or environmental elements that move across the screen, commonly seen in side-scrolling games.

### Pillar Creation
- **Random Height**: The height of each pillar is randomized using `Phaser.Math.Between(100, 300)`, which generates a value between 100 and 300 pixels. This adds variety to the game, making each pillar unique.
- **Adding the Pillar**: A new sprite is created using `this.add.sprite`, positioned at the far right of the game canvas (`game.config.width`) and aligned vertically just above the base (`game.config.height - base.height`). The `'piller'` key refers to the preloaded texture for the pillar.
- **Adjusting Dimensions**: The `displayHeight` property is set to the randomly generated height, scaling the pillar vertically. The `setOrigin(0.5, 1)` method aligns the pillar's origin to its bottom center, ensuring it grows upward from the base.

### Physics and Movement
- **Physics Body**: The pillar is added to the physics system using `this.physics.add.existing(piller)`, enabling it to interact with other physics-enabled objects.
- **Horizontal Movement**: The `setVelocityX(-100)` method gives the pillar a constant leftward velocity of 100 pixels per second, making it move across the screen.

### Cleanup
- **Out-of-Bounds Removal**: To prevent memory leaks, the pillar is destroyed when it moves out of bounds. This is achieved by enabling `onWorldBounds` and listening for the `worldbounds` event. When the pillar's physics body triggers this event, it is destroyed using `piller.destroy()`.

### Timed Creation
Finally, a Phaser `time.addEvent` is used to repeatedly call the `createPiller` function every 2 seconds (`delay: 2000`). The `loop: true` property ensures that this event continues indefinitely, creating a steady stream of pillars.

### Summary
This code dynamically generates moving pillars at random heights, adds them to the physics system, and ensures they are removed when no longer visible. The timed creation of pillars introduces a continuous challenge for the player, making it suitable for games like endless runners or side-scrolling obstacle courses.

---

```javascript
// Gravity effect to make the bird fall down
bird.y += 2; // Adjust the gravity speed as needed

// Prevent the bird from falling below the base
let baseTop = game.config.height - base.height;
if (bird.y + bird.height / 2 > baseTop) {
  bird.y = baseTop - bird.height / 2;
}
```

This code snippet simulates a gravity effect for a bird sprite in a Phaser 3 game and ensures that the bird does not fall below the base of the game scene.

### Gravity Effect
The line `bird.y += 2` increases the bird's vertical position (`y`) by 2 pixels on each frame, simulating the effect of gravity pulling the bird downward. The value `2` represents the speed of the gravity effect and can be adjusted to make the bird fall faster or slower, depending on the desired gameplay mechanics.

### Preventing the Bird from Falling Below the Base
To ensure the bird does not fall below the base of the game, the code calculates the top edge of the base using `game.config.height - base.height`. This value, stored in the variable `baseTop`, represents the vertical position where the base begins.

The `if` condition checks whether the bottom edge of the bird (`bird.y + bird.height / 2`) has moved below the top of the base (`baseTop`). If this condition is true, the bird's position is corrected by setting its `y` coordinate to `baseTop - bird.height / 2`. This adjustment ensures that the bird's bottom edge aligns perfectly with the top of the base, preventing it from visually overlapping or falling through the base.

### Summary
This code creates a realistic gravity effect for the bird while enforcing a boundary to keep it above the base. This is a common mechanic in games where objects need to interact with a ground or platform, ensuring smooth gameplay and preventing unintended behavior.
```
