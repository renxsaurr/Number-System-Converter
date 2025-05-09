# Number-System-Converter

import java.util.Scanner;

public class NumberSystemConverter {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        while (true) {
            System.out.println("\n--- Number System Converter & Calculator ---");
            System.out.println("1. Convert Number Between Systems");
            System.out.println("2. Perform Arithmetic Operations");
            System.out.println("3. Exit");
            System.out.print("Choose an option: ");
            int choice = sc.nextInt();
            sc.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    convertMenu(sc);
                    break;
                case 2:
                    arithmeticMenu(sc);
                    break;
                case 3:
                    System.out.println("Exiting program.");
                    return;
                default:
                    System.out.println("Invalid choice.");
            }
        }
    }

    static void convertMenu(Scanner sc) {
        System.out.println("\nSelect Input Base:");
        System.out.println("1. Binary");
        System.out.println("2. Decimal");
        System.out.println("3. Octal");
        System.out.println("4. Hexadecimal");
        System.out.print("Choice: ");
        int baseChoice = sc.nextInt();
        sc.nextLine(); // consume newline

        int base = switch (baseChoice) {
            case 1 -> 2;
            case 2 -> 10;
            case 3 -> 8;
            case 4 -> 16;
            default -> {
                System.out.println("Invalid base.");
                yield -1;
            }
        };
        if (base == -1) return;

        System.out.print("Enter the number: ");
        String input = sc.nextLine();

        try {
            int decimal = Integer.parseInt(input, base);
            System.out.println("\nConverted Values:");
            System.out.println("Decimal: " + decimal);
            System.out.println("Binary: " + Integer.toBinaryString(decimal));
            System.out.println("Octal: " + Integer.toOctalString(decimal));
            System.out.println("Hexadecimal: " + Integer.toHexString(decimal).toUpperCase());
        } catch (NumberFormatException e) {
            System.out.println("Invalid number format for the chosen base.");
        }
    }

    static void arithmeticMenu(Scanner sc) {
        System.out.print("\nEnter first number: ");
        String num1 = sc.next();
        System.out.print("Enter its base (2/8/10/16): ");
        int base1 = sc.nextInt();

        System.out.print("Enter second number: ");
        String num2 = sc.next();
        System.out.print("Enter its base (2/8/10/16): ");
        int base2 = sc.nextInt();

        int val1, val2;
        try {
            val1 = Integer.parseInt(num1, base1);
            val2 = Integer.parseInt(num2, base2);
        } catch (NumberFormatException e) {
            System.out.println("Invalid number format.");
            return;
        }

        System.out.println("\nSelect Operation:");
        System.out.println("1. Add\n2. Subtract\n3. Multiply\n4. Divide");
        System.out.print("Choice: ");
        int op = sc.nextInt();

        int result = 0;
        boolean valid = true;

        switch (op) {
            case 1 -> result = val1 + val2;
            case 2 -> result = val1 - val2;
            case 3 -> result = val1 * val2;
            case 4 -> {
                if (val2 == 0) {
                    System.out.println("Cannot divide by zero.");
                    valid = false;
                } else {
                    result = val1 / val2;
                }
            }
            default -> {
                System.out.println("Invalid operation.");
                valid = false;
            }
        }

        if (valid) {
            System.out.println("\nResult in:");
            System.out.println("Decimal: " + result);
            System.out.println("Binary: " + Integer.toBinaryString(result));
            System.out.println("Octal: " + Integer.toOctalString(result));
            System.out.println("Hexadecimal: " + Integer.toHexString(result).toUpperCase());
        }
    }
}
