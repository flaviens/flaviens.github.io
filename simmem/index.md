## Simulated memory controller

A Google Summer of Code 2020 project for [LowRisc CIC](https://www.lowrisc.org/), supervised by [Greg Chadwick](https://github.com/GregAC), [Pirmin Vogel](https://github.com/vogelpi) and [Alex Bradbury](https://github.com/asb).

### Context

As the gap between CPU and main memory frequency has dramatically increased in the past decades, a CPU typically interacts with a relatively slow main memory, which requires a considerable number of cycles to output data.

This is one reason why benchmarking a CPU core on a FPGA is a delicate task.
As the soft core frequency is reduced compared to an ASIC implementation, its main memory may respond much faster than in typical ASIC operation.
Additionally, there is no straightforward way to emulate a specific main memory configuration.

### Objective

The objective of this project has been to produce a configurable, synthesizable module to put between an AXI master (typically a CPU) and an AXI slave (a memory controller) port.
The module slows down the message's arrival to the requester by a delay following a configurable and realistic slower memory controller timing.

The simulated memory controller module is inserted between the _requester_ (typically the CPU) and the (real) _memory controller_.

<figure class="image">
  <img src="https://i.imgur.com/d8Mdtiu.png" alt="Overview">
  <figcaption>Fig: Simulated memory controller integration</figcaption>
</figure>

### Deliverables

The [project repository](https://github.com/lowRISC/gsoc-sim-mem) contains:
* Parametrizable synthesisable Register Transfer Level code describing a simulated memory controller.
* [Documentation](https://github.com/lowRISC/gsoc-sim-mem/blob/master/documentation.md) describing the functionality in details and how to extend it.
* Testbenches, re-usable to validate extensions to the simulated memory controller.
* A manual to integrate the simulated memory controller with a [MicroBlaze soft core](https://www.xilinx.com/products/design-tools/microblaze.html) with Xilinx Vivado.

### Future work

The current simulated memory controller can be extended in multiple documented ways, notably:

* The message delays may be calculated in different ways. The simulated memory controller integrates the [First-Ready First Come First Served delay calculation strategy, which is widely used](http://www-personal.umich.edu/~sphadke/docs/thesis.pdf), but can be adapted to other delay calculation strategies.
* Concurrent processing of multiple requests in separate banks on a single memory channel is not supported yet.
* Resource usage can be optimized, depending on other extensions.

The integration in Xilinx Vivado still encounters some problems.
This is the object of a [specific issue](https://github.com/lowRISC/gsoc-sim-mem/issues/18).

The future work is more precisely described at the end of the [project documentation](https://github.com/lowRISC/gsoc-sim-mem/blob/master/documentation.md).
