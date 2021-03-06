Usage
------

To install the library:
```
# pip install pandacan
```

See [this class](https://github.com/commaai/panda/blob/master/python/__init__.py#L80) for how to interact with the panda.

For example, to receive CAN messages:
```
>>> from panda import Panda
>>> panda = Panda()
>>> panda.can_recv()
```
And to send one on bus 0:
```
>>> panda.can_send(0x1aa, "message", 0)
```
More examples coming soon

Software interface support
------

As a universal car interface, it should support every reasonable software interface.

- User space ([done](https://github.com/commaai/panda/tree/master/python))
- socketcan in kernel ([alpha](https://github.com/commaai/panda/tree/master/drivers/linux))
- ELM327 ([done](https://github.com/commaai/panda/blob/master/boardesp/elm327.c))
- Windows J2534 ([done](https://github.com/commaai/panda/tree/master/drivers/windows))

Directory structure
------

- board      -- Code that runs on the STM32
- boardesp   -- Code that runs on the ESP8266
- drivers    -- Drivers (not needed for use with python)
- python     -- Python userspace library for interfacing with the panda
- tests      -- Tests and helper programs for panda

Programming (over USB)
------

[Programming the Board (STM32)](board/README.md)

[Programming the ESP](boardesp/README.md)


Debugging
------

To print out the serial console from the STM32, run tests/debug_console.py

To print out the serial console from the ESP8266, run PORT=1 tests/debug_console.py

Safety Model
------

When a panda powers up, by default it's in "SAFETY_NOOUTPUT" mode. While in no output mode, the buses are also forced to be silent. In order to send messages, you have to select a safety mode. Currently, setting safety modes is only supported over USB.

Safety modes can also optionally support "controls_allowed", which allows or blocks a subset of messages based on a piece of state in the board.

Hardware
------

Check out the hardware [guide](https://github.com/commaai/panda/blob/master/docs/guide.pdf)

Licensing
------

panda software is released under the MIT license unless otherwise specified.
