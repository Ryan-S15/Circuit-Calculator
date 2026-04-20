# Circuit-Calculator

#include <iostream>
using namespace std;

// Function stated
void totalSeriesResistance(float resistors[], int size);
void totalParallelResistance(float resistors[], int size);
void voltageDropSeries(float resistors[], int size, float totalVoltage);
void currentParallel(float resistors[], int size, float totalVoltage);

int main() {
    int n;
    float voltage;
// asks user for number of resistors
    cout << "Enter number of resistors: ";
    cin >> n;

    float resistors[100];
// asks user for resistor values
    cout << "Enter resistor values (ohms):\n";
    for (int i = 0; i < n; i++) {
        cin >> resistors[i];
    }
// asks user for total voltage
    cout << "Enter total voltage: ";
    cin >> voltage;

    cout << "\n--- Series Circuit ---\n";
    totalSeriesResistance(resistors, n);
    voltageDropSeries(resistors, n, voltage);

    cout << "\n--- Parallel Circuit ---\n";
    totalParallelResistance(resistors, n);
    currentParallel(resistors, n, voltage);

    return 0;
}

// Function definitions

// Calculates total resistance in a series circuit
// In series: resistances add together
void totalSeriesResistance(float resistors[], int size) {
    float total = 0;

    // Loop through all resistors and add them
    for (int i = 0; i < size; i++) {
        total += resistors[i];
    }

    // Output the final total resistance
    cout << "Total Resistance (Series): " << total << " ohms" << endl;
}

// Calculates total resistance in a parallel circuit
// Formula: 1 / (1/R1 + 1/R2 + ... + 1/Rn)
void totalParallelResistance(float resistors[], int size) {
    float reciprocalSum = 0;

    // Add the reciprocal (1/R) of each resistor
    for (int i = 0; i < size; i++) {
        reciprocalSum += 1 / resistors[i];
    }

    // Take the reciprocal of the sum to get total resistance
    float total = 1 / reciprocalSum;

    // Output the result
    cout << "Total Resistance (Parallel): " << total << " ohms" << endl;
}

// Calculates voltage drop across each resistor in a series circuit
// Uses the voltage divider rule: V_i = (R_i / R_total) * V_total
void voltageDropSeries(float resistors[], int size, float totalVoltage) {
    float totalResistance = 0;

    // First find total resistance
    for (int i = 0; i < size; i++) {
        totalResistance += resistors[i];
    }

    cout << "\nVoltage Drop across each resistor (Series):\n";

    // Calculate and display voltage drop for each resistor
    for (int i = 0; i < size; i++) {
        float voltageDrop = (resistors[i] / totalResistance) * totalVoltage;
        cout << "Resistor " << i + 1 << ": " << voltageDrop << " V" << endl;
    }
}

// Calculates current through each resistor in a parallel circuit
// Uses Ohm’s Law: I = V / R
// In parallel: voltage is the same across each resistor
void currentParallel(float resistors[], int size, float totalVoltage) {
    cout << "\nCurrent through each resistor (Parallel):\n";

    // Loop through each resistor and calculate its current
    for (int i = 0; i < size; i++) {
        float current = totalVoltage / resistors[i];

        // Output current for each resistor
        cout << "Resistor " << i + 1 << ": " << current << " A" << endl;
    }
}
