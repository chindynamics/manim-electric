# manim-electric
manim-electric is a Python library designed to simplify the creation and animation of electrical circuits using Manim. This library provides a modular architecture that includes reusable classes for common circuit elements such as voltage sources, resistors, and wires. By utilizing semantic terminal definitions for each component, circuitEasy allows you to connect elements precisely without having to manipulate numerical coordinates directly.

manim-electric is built to be flexible and scalable, enabling the addition of new components such as capacitors, inductors, or switches with minimal changes to the core connection logic. The design encourages further enhancements, including improved node grouping and advanced wiring functionalities, making it an excellent tool for educators, students, and anyone interested in visualizing electrical circuits. The project welcomes contributions from the community; developers are encouraged to open issues and submit pull requests to enhance functionality or improve documentation. Distributed under the MIT License, manim-electrical is open, accessible, and free to use for both personal and commercial projects.

## Roadmap

**Under development**
The initial release of manim-electric is planned for late June, as I balance this project with university. My goal is to maintain and evolve this library into a comprehensive toolkit for animating electrical circuits in Manim. Community support and contributions will be essential, if you’re passionate about electrical animations, your ideas, feedback, and pull requests are highly welcome!

# Documentation

## CircuitElement (Class)

This is the base class for all circuit components. It provides a dictionary called terminals to store terminal Mobjects along with a position type (such as "start", "end", or "center"). Use the method get_terminal(side) to retrieve the position of the specified terminal (for example, component.get_terminal("top") returns the top terminal’s coordinate). The method connect_to(target, target_side, self_side, animate=False) shifts the current component so that its terminal specified by self_side aligns with the terminal of the target specified by target_side. For instance, calling resistor.connect_to(vs, target_side="bottom", self_side="left", animate=False) will move the resistor so that its left terminal touches the bottom terminal of the voltage source.

## VoltageSource (Class)

This subclass of CircuitElement represents a voltage source. When instantiated (for example, VoltageSource(label="V_1")), it creates a circle to represent the source along with a label positioned to its left and a set of symbols (“+” and “–”) arranged vertically in the center. It defines two terminals—“top” and “bottom”—which you can access via get_terminal("top") or get_terminal("bottom"). A typical usage might be: vs = VoltageSource(label="V_1").move_to(LEFT * 3).

## Resistor (Class)

The Resistor class represents a resistor using an American zigzag style. It accepts parameters for label and orientation (which can be "horizontal" or "vertical"). In horizontal orientation, the resistor registers its terminals as “left” and “right”; in vertical orientation, it registers them as “top” and “bottom”. Instantiate it with a command such as Resistor(label="R_1") or Resistor(label="R_1", orientation="vertical"). Once created, you can connect it to other components using the inherited connect_to() method.

## Wire (Class)

A Wire is also a CircuitElement that represents a cable or connection. It is created by specifying a starting point and a shift vector that determines its endpoint. For example, Wire(vs.get_terminal("top"), shift_vector=RIGHT * 3, color=WHITE) creates a cable that starts from the voltage source’s top terminal and extends three units to the right. It registers its own "start" and "end" terminals, allowing you to connect other components to its ends via connect_to().

## get_terminals_position (Function)

This function accepts a component (such as a VoltageSource or Resistor) and prints (and returns) a dictionary of its terminal positions. For example, calling get_terminals_position(vs) will print the coordinates of the voltage source’s “top” and “bottom” terminals. This is useful for debugging and verifying that components are aligned as expected.

