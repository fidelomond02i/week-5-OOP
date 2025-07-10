# week-5-OOP
Create a class representing anything you like (a Smartphone, Book, or even a Superhero!).
Add attributes and methods to bring the class to life!
Use constructors to initialize each object with unique values.
Add an inheritance layer to explore polymorphism or encapsulation.
Activity 2: Polymorphism Challenge! 🎭

Create a program that includes animals or vehicles with the same action (like move()). However, make each class define move() differently (for example, Car.move() prints "Driving" 🚗, while Plane.move() prints "Flying" ✈️).
import random

# --- Base Class: Superhero ---
class Superhero:
    """
    Represents a generic superhero with fundamental attributes and abilities.
    """
    def __init__(self, name, secret_identity, powers, catchphrase="For justice!", health=100, energy=100):
        """
        Constructor for the Superhero class.

        Args:
            name (str): The superhero's public name.
            secret_identity (str): The superhero's civilian identity.
            powers (list): A list of strings representing the superhero's powers.
            catchphrase (str, optional): A unique saying. Defaults to "For justice!".
            health (int, optional): Current health points. Defaults to 100.
            energy (int, optional): Current energy points for powers. Defaults to 100.
        """
        self.name = name
        self.secret_identity = secret_identity
        self.powers = powers  # Encapsulated as a list attribute
        self.catchphrase = catchphrase
        self.health = health
        self.energy = energy
        print(f"🦸‍♂️ {self.name} (aka {self.secret_identity}) has joined the fight!")

    def display_info(self):
        """Displays the superhero's key information."""
        print(f"\n--- {self.name}'s Profile ---")
        print(f"Secret Identity: {self.secret_identity}")
        print(f"Powers: {', '.join(self.powers) if self.powers else 'None'}")
        print(f"Health: {self.health}/100")
        print(f"Energy: {self.energy}/100")
        print(f"Catchphrase: '{self.catchphrase}'")

    def use_power(self, power_name):
        """
        Simulates using a specific power.
        Checks if the superhero has the power and enough energy.
        """
        if power_name in self.powers:
            if self.energy >= 20: # Assuming 20 energy cost per power
                self.energy -= 20
                print(f"{self.name} unleashes {power_name}!")
                print(f"Energy remaining: {self.energy}")
                return True
            else:
                print(f"{self.name} is too exhausted to use {power_name}!")
                return False
        else:
            print(f"{self.name} does not possess the power of {power_name}.")
            return False

    def take_damage(self, amount):
        """Reduces health and prints status."""
        self.health -= amount
        if self.health < 0:
            self.health = 0
        print(f"💥 {self.name} took {amount} damage! Health is now {self.health}.")
        if self.health == 0:
            print(f"🚑 {self.name} is defeated!")

    def recharge_energy(self, amount):
        """Restores energy."""
        self.energy += amount
        if self.energy > 100:
            self.energy = 100
        print(f"⚡ {self.name} recharges energy by {amount}. Energy is now {self.energy}.")

    def heroic_act(self):
        """A generic heroic act that can be specialized by subclasses."""
        print(f"{self.name} performs a heroic act of bravery!")

# --- Inheritance Layer: Specialized Superheroes ---

class FlyingHero(Superhero):
    """
    A specialized superhero with flying abilities.
    Inherits from Superhero.
    """
    def __init__(self, name, secret_identity, powers, flight_speed_mph, catchphrase="Up, up, and away!", health=100, energy=100):
        # Call the parent class's constructor to initialize common attributes
        super().__init__(name, secret_identity, powers + ["Flight"], catchphrase, health, energy)
        self.flight_speed_mph = flight_speed_mph # New attribute for FlyingHero
        # Encapsulation: A 'private' attribute for internal use
        self._altitude = 0 # Starting altitude

    def display_info(self):
        """Overrides the parent's display_info to add flight specific info."""
        super().display_info() # Call parent's method to print common info
        print(f"Flight Speed: {self.flight_speed_mph} mph")
        print(f"Current Altitude: {self._altitude} feet") # Displaying the encapsulated attribute

    def take_off(self):
        """Simulates taking off."""
        if self.energy >= 10:
            self.energy -= 10
            self._altitude = 500 # Set initial altitude
            print(f"🚀 {self.name} gracefully takes to the skies! Energy: {self.energy}")
        else:
            print(f"🪫 {self.name} is too tired to take off.")

    def land(self):
        """Simulates landing."""
        if self._altitude > 0:
            self._altitude = 0
            print(f"🛬 {self.name} has safely landed.")
        else:
            print(f"{self.name} is already on the ground.")

    def heroic_act(self):
        """Polymorphism: Overrides the generic heroic_act for flying heroes."""
        if self.use_power("Flight"):
            print(f"🌟 {self.name} soars through the sky, rescuing citizens from danger!")
            self.land()
        else:
            print(f"{self.name} tries to fly, but needs more energy!")

class StrengthHero(Superhero):
    """
    A specialized superhero with enhanced strength.
    Inherits from Superhero.
    """
    def __init__(self, name, secret_identity, powers, strength_level, catchphrase="Unstoppable!", health=100, energy=100):
        super().__init__(name, secret_identity, powers + ["Super Strength"], catchphrase, health, energy)
        self.strength_level = strength_level # New attribute for StrengthHero

    def display_info(self):
        """Overrides the parent's display_info to add strength specific info."""
        super().display_info() # Call parent's method to print common info
        print(f"Strength Level: {self.strength_level} (out of 10)")

    def lift_heavy_object(self, object_weight):
        """Simulates lifting a heavy object."""
        if self.strength_level * 100 >= object_weight: # Simple logic
            if self.energy >= 15:
                self.energy -= 15
                print(f"💪 {self.name} effortlessly lifts a {object_weight}kg object! Energy: {self.energy}")
                return True
            else:
                print(f"🪫 {self.name} is too tired to lift that!")
                return False
        else:
            print(f"😬 {self.name} struggles. {object_weight}kg is a bit too heavy for this strength level.")
            return False

    def heroic_act(self):
        """Polymorphism: Overrides the generic heroic_act for strength heroes."""
        if self.lift_heavy_object(random.randint(500, 2000)): # Lift a random heavy object
            print(f"🔥 {self.name} smashes through obstacles, saving the day with raw power!")
        else:
            print(f"{self.name} needs more power for this heroic feat!")

# --- Demonstration of Assignment 1 ---
print("--- Assignment 1: Design Your Own Class (Superhero) ---")

# Create instances of the classes
hero_prime = Superhero(
    "Captain Code",
    "Alice Smith",
    ["Tactical Planning", "Gadgetry"],
    "Code is my weapon!"
)

fly_guy = FlyingHero(
    "Sky Guardian",
    "Bob Johnson",
    ["Enhanced Vision"],
    flight_speed_mph=700,
    catchphrase="The sky calls!"
)

mega_muscle = StrengthHero(
    "Titan",
    "Carol Davis",
    ["Invulnerability"],
    strength_level=9,
    health=120 # Titan has more health!
)

# Use methods and display info
hero_prime.display_info()
hero_prime.use_power("Gadgetry")
hero_prime.take_damage(30)
hero_prime.recharge_energy(10)
hero_prime.heroic_act()


fly_guy.display_info()
fly_guy.take_off()
fly_guy.use_power("Enhanced Vision")
fly_guy.heroic_act() # Polymorphic call - calls FlyingHero's heroic_act
fly_guy.take_damage(50)
fly_guy.land()

mega_muscle.display_info()
mega_muscle.lift_heavy_object(800)
mega_muscle.take_damage(10)
mega_muscle.heroic_act() # Polymorphic call - calls StrengthHero's heroic_act
mega_muscle.use_power("Super Strength")
mega_muscle.take_damage(120) # Simulate defeat
print("-" * 50)
