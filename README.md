# system_monitoring_tool

1. How the Problem Was Solved

The objective was to create a real-time system monitoring tool in C that reports memory usage, CPU utilization, and core information dynamically, with graphical representation. The solution was implemented using various system APIs and ANSI escape codes to update the terminal display in real-time. Key features include:

Real-time monitoring using loops and usleep() for time delays.

Dynamic graphs to visualize CPU and memory usage.

Parsing command-line arguments to control displayed metrics.

Efficient system calls to retrieve memory, CPU, and core data.

Formatted terminal output with ANSI escape codes for a structured display.

2. Overview of Functions and Documentation

2.1 Program Configuration & Parsing Arguments

parse_arguments(int argc, char *argv[], ProgramSettings *settings)

Parses command-line arguments to determine what metrics should be displayed.

Uses getopt_long() for flexible argument parsing.

Supports --memory, --cpu, --cores, --samples, and --tdelay flags.

2.2 Data Collection Functions

double get_memory_usage(void)

Uses sysinfo() to fetch total and used memory.

Converts memory values into gigabytes for better readability.

double get_cpu_usage(void)

Reads /proc/stat to calculate CPU usage percentage over time.

Uses a rolling difference method to compute CPU utilization.

int get_core_count(void)

Uses sysconf(_SC_NPROCESSORS_ONLN) to detect the number of available CPU cores.

double get_cpu_freq(void)

Reads /proc/cpuinfo to fetch the CPU frequency in GHz.

2.3 Graph and Display Functions

void draw_memory_graph(SystemStats *stats)

Prints a bar graph representing memory usage over time.

Uses # symbols to indicate memory levels.

void draw_cpu_graph(SystemStats *stats)

Displays a bar graph showing CPU usage.

Uses : symbols to represent utilization.

void display_cores_info(void)

Prints a grid structure representing the detected CPU cores.

Uses +---+ ASCII boxes to display core layouts.

void clear_screen(void)

Uses ANSI escape codes (\033[2J\033[H) to clear the terminal screen before each update.

2.4 Main Execution Flow

The main() function initializes settings, processes arguments, and enters a monitoring loop.

Inside the loop, memory and CPU stats are collected, and graphs are displayed.

The loop repeats for the specified number of samples with a time delay (usleep(tdelay)).

3. How to Run the Program

3.1 Compilation

To compile the program, use:

gcc -o myMonitoringTool system_monitoring_tool.c

3.2 Running the Program

The tool accepts command-line arguments:

./myMonitoringTool [samples] [tdelay] [--memory] [--cpu] [--cores]

Example Usage:

Default behavior (monitors everything for 20 samples, 0.5s delay)

./myMonitoringTool

Monitor only memory usage

./myMonitoringTool --memory

Monitor only CPU usage

./myMonitoringTool --cpu

Monitor everything with custom samples and delay

./myMonitoringTool 50 1000000  # 50 samples, 1s delay

4. Conclusion

This program effectively provides real-time insights into system performance metrics. The implementation prioritizes efficiency and clarity, using structured ANSI-based visualization, modular code design, and robust argument parsing. Future improvements could include logging capabilities, additional system metrics, and a graphical interface for better visualization.
