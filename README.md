# Appendix for "How Does Experience Influence Developer Perceptions of Atoms of Confusion?"

Here we list an example task with a defective code snippet containing AoCs and the three fixes.

Note: We might update the examples as we will refine the experiment design after a pilot study.

## Defective code snippet
Note: The comments are there for clarification. There will not be such comments in the actual experiment.
```
public class NumberUtilsBuggy {
    public static boolean isInRange(int x, int min, int maxExclusive, boolean inclusive) {
        // Bug: the ternary operator and && precedence misleads readers
        return inclusive ? x >= min && x < maxExclusive : x > min && x < maxExclusive;
    }

    public static void main(String[] args) {
        int testValue = 10;
        int lower = 5;
        int upper = 10;

        System.out.println("Result: " + isInRange(testValue, lower, upper, false));
        // ❌ Expected false, but prints true
    }
}
```

### Fix 1
This fix keeps the AoC but is shorter.
```
public class NumberUtilsBuggy {
    public static boolean isInRange(int x, int min, int maxExclusive, boolean inclusive) {
        // Bug: the ternary operator and && precedence misleads readers
        return inclusive ? x >= min && x < maxExclusive : x > min && x < maxExclusive;
    }

    public static void main(String[] args) {
        int testValue = 10;
        int lower = 5;
        int upper = 10;

        System.out.println("Result: " + isInRange(testValue, lower, upper, false));
        // ❌ Expected false, but prints true
    }
}
```

### Fix 2
This fix removes the AoC but is longer.
```
public class NumberUtilsFix2 {
    public static boolean isInRange(int x, int min, int maxExclusive, boolean inclusive) {
        // No AoC — clear and explicit
        if (inclusive) {
            return x >= min && x < maxExclusive;
        } else {
            return x > min && x < maxExclusive;
        }
    }

    public static void main(String[] args) {
        int testValue = 10;
        int lower = 5;
        int upper = 10;

        System.out.println("Result: " + isInRange(testValue, lower, upper, false));
        // ✅ Prints false as expected
    }
}
```

### Fix 3
This fix adds another AoC but is shorter.
```
public class NumberUtilsFix3 {
    public static boolean isInRange(int x, int min, int maxExclusive, boolean inclusive) {
        // Adds CLE AoC: (inclusive ? 0 : 1) + x > min
        return ((inclusive ? 0 : 1) + x > min) && x < maxExclusive;
    }

    public static void main(String[] args) {
        int testValue = 10;
        int lower = 5;
        int upper = 10;

        System.out.println("Result: " + isInRange(testValue, lower, upper, false));
        // ✅ Prints false as expected
    }
}
```
