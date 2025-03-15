# TOP 50 STRING INTERVIEW QUESTIONS WITH SOLUTIONS IN JAVA

## Basic String Operations

### 1. How do you declare and initialize a String in Java?
```java
// Declaration and initialization
String str1 = "Hello";             // Using string literal
String str2 = new String("Hello"); // Using new keyword

// Empty string
String empty = "";

// String from char array
char[] charArray = {'H', 'e', 'l', 'l', 'o'};
String str3 = new String(charArray);

// String from byte array
byte[] byteArray = {72, 101, 108, 108, 111};
String str4 = new String(byteArray);

// String from StringBuilder or StringBuffer
StringBuilder sb = new StringBuilder("Hello");
String str5 = sb.toString();
```

### 2. What is the difference between String, StringBuilder, and StringBuffer in Java?
```java
// String is immutable - once created, cannot be modified
String str = "Hello";
str = str + " World"; // Creates a new string object, doesn't modify original

// StringBuilder is mutable, not thread-safe, but faster
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies the original object

// StringBuffer is mutable and thread-safe (synchronized), but slower
StringBuffer sbf = new StringBuffer("Hello");
sbf.append(" World"); // Modifies the original object in a thread-safe way

// Performance demonstration
long startTime = System.currentTimeMillis();

// String concatenation
String s = "";
for (int i = 0; i < 10000; i++) {
    s += "a"; // Creates 10000 string objects
}

// vs StringBuilder
StringBuilder sb2 = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    sb2.append("a"); // Modifies the same object
}
String result = sb2.toString(); // Only creates one new string
```

### 3. How do you compare two strings in Java?
```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

// Using == operator (compares object references)
boolean b1 = (str1 == str2);      // true (string literals share the same reference)
boolean b2 = (str1 == str3);      // false (different objects in memory)

// Using equals() method (compares content)
boolean b3 = str1.equals(str2);   // true
boolean b4 = str1.equals(str3);   // true

// Using equalsIgnoreCase() (ignores case differences)
boolean b5 = "hello".equalsIgnoreCase("Hello");  // true

// Using compareTo() method (lexicographical comparison)
int result1 = "apple".compareTo("banana");  // negative value (a comes before b)
int result2 = "banana".compareTo("apple");  // positive value (b comes after a)
int result3 = "apple".compareTo("apple");   // 0 (equal strings)

// Using compareToIgnoreCase() method
int result4 = "APPLE".compareToIgnoreCase("apple");  // 0 (ignores case)
```

### 4. How to check if a string is empty or null in Java?
```java
String str = null;
String emptyStr = "";
String blankStr = "   ";

// Checking for null
boolean isNull = (str == null);  // true

// Checking for empty string
boolean isEmpty1 = (emptyStr != null && emptyStr.length() == 0);  // true
boolean isEmpty2 = (emptyStr != null && emptyStr.isEmpty());      // true (Java 6+)

// Checking for null or empty
boolean isNullOrEmpty = (str == null || str.isEmpty());  // true

// Checking for blank string (null, empty, or just whitespace)
boolean isBlank1 = (blankStr != null && blankStr.trim().isEmpty());  // true
boolean isBlank2 = (blankStr != null && blankStr.isBlank());         // true (Java 11+)

// Using Apache Commons Lang (if available)
// boolean isEmptyCommons = StringUtils.isEmpty(str);  // true for null or empty
// boolean isBlankCommons = StringUtils.isBlank(str);  // true for null, empty, or whitespace
```

### 5. How to reverse a string in Java?
```java
// Method 1: Using StringBuilder/StringBuffer
public static String reverseString1(String str) {
    if (str == null || str.isEmpty()) {
        return str;
    }
    return new StringBuilder(str).reverse().toString();
}

// Method 2: Using character array
public static String reverseString2(String str) {
    if (str == null || str.isEmpty()) {
        return str;
    }
    
    char[] chars = str.toCharArray();
    int left = 0;
    int right = chars.length - 1;
    
    while (left < right) {
        // Swap characters
        char temp = chars[left];
        chars[left] = chars[right];
        chars[right] = temp;
        
        // Move indices
        left++;
        right--;
    }
    
    return new String(chars);
}

// Method 3: Using recursion
public static String reverseString3(String str) {
    if (str == null || str.length() <= 1) {
        return str;
    }
    return reverseString3(str.substring(1)) + str.charAt(0);
}

// Method 4: Using Java 8 Streams
public static String reverseString4(String str) {
    if (str == null || str.isEmpty()) {
        return str;
    }
    
    return str.chars()
              .mapToObj(c -> (char) c)
              .reduce("", (s, c) -> c + s, (s1, s2) -> s2 + s1);
}
```

### 6. How to convert String to char array and vice versa?
```java
// String to char array
String str = "Hello World";
char[] charArray = str.toCharArray();

// Accessing individual characters
for (char c : charArray) {
    System.out.println(c);
}

// Getting a specific character
char fifthChar = str.charAt(4);  // 'o'

// Char array to String
char[] chars = {'H', 'e', 'l', 'l', 'o'};
String newStr = new String(chars);

// Creating a string from a portion of a char array
String partialStr = new String(chars, 1, 3);  // "ell" (start at index 1, length 3)
```

### 7. How to convert String to int and vice versa?
```java
// String to int
String numStr = "123";
int num1 = Integer.parseInt(numStr);       // Throws NumberFormatException if invalid
int num2 = Integer.valueOf(numStr);        // Returns Integer object

// String to int with handling exception
int number;
try {
    number = Integer.parseInt(numStr);
} catch (NumberFormatException e) {
    number = 0;  // Default value on error
}

// int to String
int num = 123;
String str1 = Integer.toString(num);
String str2 = String.valueOf(num);
String str3 = "" + num;  // Less efficient concatenation

// Converting other number types
String doubleStr = "123.45";
double doubleVal = Double.parseDouble(doubleStr);

long longVal = Long.parseLong("123456789");
float floatVal = Float.parseFloat("123.45f");
```

### 8. How to find the length of a string in Java?
```java
String str = "Hello World";
int length = str.length();  // Returns 11

// Handle null safely
String nullStr = null;
int safeLength = (nullStr != null) ? nullStr.length() : 0;  // Returns 0
```

### 9. How to get a substring from a string in Java?
```java
String str = "Hello World";

// Get substring from start index to end of string
String sub1 = str.substring(6);     // "World"

// Get substring from start index (inclusive) to end index (exclusive)
String sub2 = str.substring(0, 5);  // "Hello"

// Handle exceptions safely
String sub3 = "";
try {
    sub3 = str.substring(20);  // Will throw IndexOutOfBoundsException
} catch (IndexOutOfBoundsException e) {
    sub3 = "";  // Default on error
}

// Get last N characters
int n = 3;
String lastChars = str.substring(Math.max(0, str.length() - n));  // "rld"
```

### 10. How to trim a string in Java?
```java
String str = "   Hello World   ";

// Remove leading and trailing whitespace
String trimmed = str.trim();  // "Hello World"

// Java 11+ strip methods (also handles Unicode whitespace)
String stripped = str.strip();        // Removes whitespace from both ends
String stripLeading = str.stripLeading();  // Removes from beginning
String stripTrailing = str.stripTrailing();  // Removes from end

// Custom trim for non-whitespace characters
String customTrim = str.replaceAll("^[^a-zA-Z0-9]+|[^a-zA-Z0-9]+$", "");
```

## String Manipulation

### 11. How to replace characters in a string in Java?
```java
String str = "Hello World";

// Replace a single character
String replaced1 = str.replace('l', 'x');  // "Hexxo Worxd"

// Replace a substring
String replaced2 = str.replace("Hello", "Hi");  // "Hi World"

// Replace first occurrence of a regex pattern
String replaced3 = str.replaceFirst("l", "x");  // "Hexlo World"

// Replace all occurrences of a regex pattern
String replaced4 = str.replaceAll("l", "x");    // "Hexxo Worxd"

// Replace with case-insensitive regex
String replaced5 = str.replaceAll("(?i)hello", "Hi");  // "Hi World"

// Complex regex replacement
String text = "My phone number is 123-456-7890";
String formatted = text.replaceAll("(\\d{3})-(\\d{3})-(\\d{4})", "($1) $2-$3");
// "My phone number is (123) 456-7890"
```

### 12. How to split a string in Java?
```java
String str = "apple,banana,orange,grape";

// Split by comma
String[] fruits = str.split(",");  // ["apple", "banana", "orange", "grape"]

// Split with limit (max number of substrings)
String[] limitedFruits = str.split(",", 2);  // ["apple", "banana,orange,grape"]

// Split by regex
String text = "Hello.World|Java;Programming";
String[] words = text.split("[.|;]");  // ["Hello", "World|Java", "Programming"]

// Split by whitespace
String sentence = "This is   a   sentence";
String[] allWords = sentence.split("\\s+");  // ["This", "is", "a", "sentence"]

// Keep delimiters using lookahead/lookbehind
String data = "1,2,3,4,5";
String[] numbersWithCommas = data.split("(?<=,)|(?=,)");
// ["1", ",", "2", ",", "3", ",", "4", ",", "5"]

// Handle empty results
String emptyParts = "a..b.c";
String[] parts1 = emptyParts.split("\\.");     // ["a", "", "b", "c"]
String[] parts2 = emptyParts.split("\\.", -1);  // ["a", "", "b", "c", ""]
```

### 13. How to convert a string to uppercase or lowercase in Java?
```java
String str = "Hello World";

// Convert to uppercase
String upper = str.toUpperCase();  // "HELLO WORLD"

// Convert to lowercase
String lower = str.toLowerCase();  // "hello world"

// Locale-specific case conversion (important for international text)
String turkishLower = str.toLowerCase(Locale.forLanguageTag("tr"));  // Turkish rules
String englishUpper = str.toUpperCase(Locale.ENGLISH);  // English rules

// First letter uppercase, rest lowercase (capitalize)
String name = "jOHN";
String capitalized = name.substring(0, 1).toUpperCase() + 
                   name.substring(1).toLowerCase();  // "John"

// Capitalize each word
String text = "hello world";
String[] words = text.split("\\s+");
StringBuilder titleCase = new StringBuilder();
for (String word : words) {
    if (!word.isEmpty()) {
        titleCase.append(Character.toUpperCase(word.charAt(0)))
                .append(word.substring(1).toLowerCase())
                .append(" ");
    }
}
String result = titleCase.toString().trim();  // "Hello World"
```

### 14. How to check if a string contains a substring in Java?
```java
String str = "Hello World";

// Using contains()
boolean contains1 = str.contains("World");  // true
boolean contains2 = str.contains("world");  // false (case-sensitive)

// Using indexOf()
boolean contains3 = str.indexOf("World") >= 0;  // true
boolean contains4 = str.indexOf("world") >= 0;  // false (case-sensitive)

// Case-insensitive check
boolean containsIgnoreCase = str.toLowerCase().contains("world".toLowerCase());  // true

// Using regex
boolean containsRegex = str.matches(".*World.*");  // true

// Check if string starts with a prefix
boolean startsWith = str.startsWith("Hello");  // true
boolean startsWithOffset = str.startsWith("World", 6);  // true (starts checking at position 6)

// Check if string ends with a suffix
boolean endsWith = str.endsWith("World");  // true
```

### 15. How to find the index of a character or substring in Java?
```java
String str = "Hello World";

// Find first occurrence of a character
int index1 = str.indexOf('o');        // 4
int index2 = str.indexOf("o");        // 4 (can use String or char)

// Find first occurrence starting from a specific position
int index3 = str.indexOf('o', 5);     // 7 (starts searching from index 5)

// Find last occurrence of a character
int lastIndex1 = str.lastIndexOf('o');  // 7

// Find last occurrence before a specific position
int lastIndex2 = str.lastIndexOf('o', 6);  // 4 (searches backwards from index 6)

// Find all occurrences
List<Integer> allOccurrences = new ArrayList<>();
int index = str.indexOf('l');
while (index >= 0) {
    allOccurrences.add(index);
    index = str.indexOf('l', index + 1);
}
// allOccurrences contains [2, 3, 9]

// Not found returns -1
int notFound = str.indexOf('z');  // -1
```

### 16. How to join strings in Java?
```java
// Using + operator (less efficient for many strings)
String str1 = "Hello" + " " + "World";

// Using String.join() (Java 8+)
String joined1 = String.join(", ", "Apple", "Banana", "Orange");  // "Apple, Banana, Orange"
String joined2 = String.join("-", new String[]{"2023", "04", "15"});  // "2023-04-15"

List<String> list = Arrays.asList("Java", "Python", "C++");
String joined3 = String.join(" | ", list);  // "Java | Python | C++"

// Using StringJoiner (Java 8+)
StringJoiner joiner = new StringJoiner(", ", "[", "]");
joiner.add("Apple").add("Banana").add("Orange");
String result = joiner.toString();  // "[Apple, Banana, Orange]"

// Using StringBuilder (most efficient for many concatenations)
StringBuilder sb = new StringBuilder();
sb.append("Hello").append(" ").append("World");
String result2 = sb.toString();  // "Hello World"

// Using Collectors.joining() with streams (Java 8+)
List<String> fruits = Arrays.asList("Apple", "Banana", "Orange");
String joined4 = fruits.stream().collect(Collectors.joining(", "));  // "Apple, Banana, Orange"
```

### 17. How to check if a string is a palindrome in Java?
```java
public static boolean isPalindrome(String str) {
    if (str == null) {
        return false;
    }
    
    // Remove non-alphanumeric characters and convert to lowercase
    String cleaned = str.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
    
    // Method 1: Using two pointers
    int left = 0;
    int right = cleaned.length() - 1;
    
    while (left < right) {
        if (cleaned.charAt(left) != cleaned.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    
    return true;
    
    /* Method 2: Using StringBuilder
    String reversed = new StringBuilder(cleaned).reverse().toString();
    return cleaned.equals(reversed);
    */
}

// Example usage
boolean test1 = isPalindrome("racecar");  // true
boolean test2 = isPalindrome("A man, a plan, a canal: Panama");  // true
boolean test3 = isPalindrome("hello");  // false
```

### 18. How to count occurrences of a character or substring in a string in Java?
```java
// Count occurrences of a character
public static int countChar(String str, char ch) {
    if (str == null || str.isEmpty()) {
        return 0;
    }
    
    int count = 0;
    for (int i = 0; i < str.length(); i++) {
        if (str.charAt(i) == ch) {
            count++;
        }
    }
    
    return count;
}

// Count occurrences of a substring
public static int countSubstring(String str, String sub) {
    if (str == null || sub == null || str.isEmpty() || sub.isEmpty()) {
        return 0;
    }
    
    // Method 1: Using indexOf()
    int count = 0;
    int index = 0;
    while ((index = str.indexOf(sub, index)) != -1) {
        count++;
        index += sub.length();
    }
    
    return count;
    
    /* Method 2: Using regex
    Pattern pattern = Pattern.compile(Pattern.quote(sub));
    Matcher matcher = pattern.matcher(str);
    
    int count = 0;
    while (matcher.find()) {
        count++;
    }
    
    return count;
    */
    
    /* Method 3: Using String.split() (works for non-overlapping matches)
    return str.split(Pattern.quote(sub), -1).length - 1;
    */
}

// Examples
int charCount = countChar("Hello World", 'l');  // 3
int subCount = countSubstring("abababa", "aba");  // 3 (overlapping matches)
```

### 19. How to remove all white spaces from a string in Java?
```java
String str = "  Hello   World  ";

// Remove all whitespace characters
String noSpaces1 = str.replaceAll("\\s", "");  // "HelloWorld"

// Remove only spaces (not tabs, newlines, etc.)
String noSpaces2 = str.replaceAll(" ", "");    // "HelloWorld"

// Remove leading and trailing spaces only
String trimmed = str.trim();  // "Hello   World"
String stripped = str.strip();  // "Hello   World" (Java 11+, handles Unicode whitespace better)

// Custom character replacement
String replaced = str.replaceAll("\\s", "-");  // "--Hello---World--"
```

### 20. How to check if a string is a valid number in Java?
```java
public static boolean isNumeric(String str) {
    if (str == null || str.isEmpty()) {
        return false;
    }
    
    // Method 1: Using regex
    return str.matches("-?\\d+(\\.\\d+)?");
    
    /* Method 2: Using exception handling
    try {
        Double.parseDouble(str);
        return true;
    } catch (NumberFormatException e) {
        return false;
    }
    */
    
    /* Method 3: Character checking
    boolean hasDecimal = false;
    
    for (int i = 0; i < str.length(); i++) {
        char c = str.charAt(i);
        
        // Check for minus sign at the beginning
        if (c == '-' && i == 0) {
            continue;
        }
        
        // Check for one decimal point
        if (c == '.') {
            if (hasDecimal) {
                return false;  // More than one decimal point
            }
            hasDecimal = true;
            continue;
        }
        
        // Check for digits
        if (!Character.isDigit(c)) {
            return false;
        }
    }
    
    return true;
    */
}

// Examples
boolean test1 = isNumeric("123");       // true
boolean test2 = isNumeric("-123.45");   // true
boolean test3 = isNumeric("123.45.67"); // false
boolean test4 = isNumeric("abc");       // false
boolean test5 = isNumeric("");          // false
boolean test6 = isNumeric("12a");       // false
```

## String Searching and Pattern Matching

### 21. How to implement string matching algorithms in Java?
```java
// Naive string matching algorithm
public static int naiveStringMatch(String text, String pattern) {
    int n = text.length();
    int m = pattern.length();
    
    for (int i = 0; i <= n - m; i++) {
        int j;
        
        // Check for pattern match starting at position i
        for (j = 0; j < m; j++) {
            if (text.charAt(i + j) != pattern.charAt(j)) {
                break;
            }
        }
        
        // If entire pattern matched
        if (j == m) {
            return i;  // Return the starting index of the match
        }
    }
    
    return -1;  // Pattern not found
}

// Rabin-Karp string matching algorithm (using hashing)
public static int rabinKarp(String text, String pattern) {
    int n = text.length();
    int m = pattern.length();
    
    // Base value for hashing (can be any prime number)
    int prime = 101;
    
    // Calculate hash of pattern and initial window of text
    int patternHash = 0;
    int textHash = 0;
    int h = 1;
    
    // Calculate h = prime^(m-1)
    for (int i = 0; i < m - 1; i++) {
        h = (h * 256) % prime;
    }
    
    // Calculate initial hash values
    for (int i = 0; i < m; i++) {
        patternHash = (256 * patternHash + pattern.charAt(i)) % prime;
        textHash = (256 * textHash + text.charAt(i)) % prime;
    }
    
    // Slide the pattern over text one by one
    for (int i = 0; i <= n - m; i++) {
        // Check if hash values match
        if (patternHash == textHash) {
            // Check for actual character match
            boolean match = true;
            for (int j = 0; j < m; j++) {
                if (text.charAt(i + j) != pattern.charAt(j)) {
                    match = false;
                    break;
                }
            }
            
            if (match) {
                return i;
            }
        }
        
        // Calculate hash for next window
        if (i < n - m) {
            textHash = (256 * (textHash - text.charAt(i) * h) + text.charAt(i + m)) % prime;
            
            // Ensure positive hash value
            if (textHash < 0) {
                textHash += prime;
            }
        }
    }
    
    return -1;  // Pattern not found
}

// Using Java's built-in String methods
public static int builtInMatch(String text, String pattern) {
    return text.indexOf(pattern);
}

// Examples
String text = "ABABDABACDABABCABAB";
String pattern = "ABABCABAB";

int result1 = naiveStringMatch(text, pattern);  // 10
int result2 = rabinKarp(text, pattern);         // 10
int result3 = builtInMatch(text, pattern);      // 10
```

### 22. How to use regular expressions in Java?
```java
// Basic regex matching
String text = "The quick brown fox jumps over the lazy dog.";
boolean containsWord = text.matches(".*fox.*");  // true

// Finding matches
Pattern pattern = Pattern.compile("\\w+");  // Match word characters
Matcher matcher = pattern.matcher(text);

while (matcher.find()) {
    String word = matcher.group();
    int start = matcher.start();
    int end = matcher.end();
    System.out.println(word + " found at positions " + start + "-" + end);
}

// Replacing with regex
String replaced = text.replaceAll("\\b\\w{4}\\b", "XXXX");  // Replace 4-letter words
// "The XXXX brown fox XXXX over the XXXX dog."

// Splitting with regex
String[] parts = text.split("\\s+");  // Split by whitespace

// Capturing groups
Pattern groupPattern = Pattern.compile("(\\d{3})-(\\d{3})-(\\d{4})");
Matcher m = groupPattern.matcher("Phone: 123-456-7890");

if (m.find()) {
    String areaCode = m.group(1);  // "123"
    String prefix = m.group(2);    // "456"
    String line = m.group(3);      // "7890"
    String fullMatch = m.group(0); // "123-456-7890"
}

// Email validation
String email = "user@example.com";
boolean isValid = email.matches("[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}");

// Replacing with backreferences
String html = "<div>Hello <b>World</b></div>";
String modified = html.replaceAll("<([a-z]+)>(.*?)</\\1>", "[$2]");
// Result: "[Hello [World]]"
```

### 23. How to match repeated patterns in a string?
```java
// Find all repeated substrings
public static List<String> findRepeatedSubstrings(String str, int minLength) {
    Set<String> result = new HashSet<>();
    Set<String> seen = new HashSet<>();
    
    for (int i = 0; i <= str.length() - minLength; i++) {
        for (int j = minLength; i + j <= str.length(); j++) {
            String substring = str.substring(i, i + j);
            if (!seen.add(substring)) {
                result.add(substring);
            }
        }
    }
    
    return new ArrayList<>(result);
}

// Find longest repeated substring
public static String longestRepeatedSubstring(String str) {
    int n = str.length();
    String result = "";
    
    // Create suffix array
    String[] suffixes = new String[n];
    for (int i = 0; i < n; i++) {
        suffixes[i] = str.substring(i);
    }
    
    // Sort suffixes
    Arrays.sort(suffixes);
    
    // Find the longest common prefix between adjacent suffixes
    for (int i = 0; i < n - 1; i++) {
        String commonPrefix = longestCommonPrefix(suffixes[i], suffixes[i + 1]);
        if (commonPrefix.length() > result.length()) {
            result = commonPrefix;
        }
    }
    
    return result;
}

private static String longestCommonPrefix(String a, String b) {
    int minLength = Math.min(a.length(), b.length());
    for (int i = 0; i < minLength; i++) {
        if (a.charAt(i) != b.charAt(i)) {
            return a.substring(0, i);
        }
    }
    return a.substring(0, minLength);
}

// Examples
String text = "ABABABA";
List<String> repeats = findRepeatedSubstrings(text, 2);
// ["ABA", "ABABA", "BAB", "BABA", "AB", "BA"]

String longest = longestRepeatedSubstring(text);  // "ABABA" or "BABA"
```

### 24. How to validate if a string matches a specific format?
```java
// Validate email address
public static boolean isValidEmail(String email) {
    String regex = "^[a-zA-Z0-9_+&*-]+(?:\\.[a-zA-Z0-9_+&*-]+)*@(?:[a-zA-Z0-9-]+\\.)+[a-zA-Z]{2,7}$";
    return Pattern.matches(regex, email);
}

// Validate phone number (US format)
public static boolean isValidPhoneNumber(String phone) {
    String regex = "^(\\+\\d{1,2}\\s?)?\\(?\\d{3}\\)?[\\s.-]?\\d{3}[\\s.-]?\\d{4}$";
    return Pattern.matches(regex, phone);
}

// Validate date (MM/DD/YYYY format)
public static boolean isValidDate(String date) {
    String regex = "^(0[1-9]|1[0-2])/(0[1-9]|[12][0-9]|3[01])/\\d{4}$";
    
    if (!Pattern.matches(regex, date)) {
        return false;
    }
    
    // Additional date validation logic
    try {
        SimpleDateFormat sdf = new SimpleDateFormat("MM/dd/yyyy");
        sdf.setLenient(false);
        sdf.parse(date);
        return true;
    } catch (ParseException e) {
        return false;
    }
}

// Validate URL
public static boolean isValidUrl(String url) {
    String regex = "^(https?|ftp|file)://[-a-zA-Z0-9+&@#/%?=~_|!:,.;]*[-a-zA-Z0-9+&@#/%=~_|]";
    return Pattern.matches(regex, url);
}

// Validate password strength
public static boolean isStrongPassword(String password) {
    // At least 8 chars, contains digits, lowercase, uppercase, and special chars
    String regex = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=])(?=\\S+$).{8,}$";
    return Pattern.matches(regex, password);
}

// Examples
boolean validEmail = isValidEmail("user@example.com");  // true
boolean validPhone = isValidPhoneNumber("(123) 456-7890");  // true
boolean validDate = isValidDate("01/30/2023");  // true
boolean validUrl = isValidUrl("https://www.example.com");  // true
boolean strongPassword = isStrongPassword("P@ssw0rd");  // true
```

### 25. How to extract all numbers from a string in Java?
```java
// Extract all numbers (including decimals)
public static List<String> extractNumbers(String text) {
    List<String> numbers = new ArrayList<>();
    Pattern pattern = Pattern.compile("[-+]?\\d*\\.?\\d+");
    Matcher matcher = pattern.matcher(text);
    
    while (matcher.find()) {
        numbers.add(matcher.group());
    }
    
    return numbers;
}

// Extract integers only
public static List<Integer> extractIntegers(String text) {
    List<Integer> numbers = new ArrayList<>();
    Pattern pattern = Pattern.compile("\\d+");
    Matcher matcher = pattern.matcher(text);
    
    while (matcher.find()) {
        try {
            numbers.add(Integer.parseInt(matcher.group()));
        } catch (NumberFormatException e) {
            // Skip if the number is too large for an integer
        }
    }
    
    return numbers;
}

// Examples
String text = "The price is $19.99 and quantity is 5. Model number is A-123-456.";

List<String> allNumbers = extractNumbers(text);
// ["19.99", "5", "123", "456"]

List<Integer> integers = extractIntegers(text);
// [19, 99, 5, 123, 456]
```

## Advanced String Topics

### 26. How to implement a custom string tokenizer in Java?
```java
public static List<String> customTokenize(String text, String delimiters) {
    List<String> tokens = new ArrayList<>();
    
    if (text == null || text.isEmpty()) {
        return tokens;
    }
    
    // Create a boolean array for quick lookup of delimiter chars
    boolean[] isDelimiter = new boolean[256];
    for (char c : delimiters.toCharArray()) {
        isDelimiter[c] = true;
    }
    
    StringBuilder token = new StringBuilder();
    
    for (char c : text.toCharArray()) {
        if (c < 256 && isDelimiter[c]) {
            // Found a delimiter
            if (token.length() > 0) {
                tokens.add(token.toString());
                token.setLength(0);  // Clear the builder
            }
        } else {
            // Add character to current token
            token.append(c);
        }
    }
    
    // Don't forget the last token
    if (token.length() > 0) {
        tokens.add(token.toString());
    }
    
    return tokens;
}

// Using Java's StringTokenizer
public static List<String> tokenizeWithStringTokenizer(String text, String delimiters) {
    List<String> tokens = new ArrayList<>();
    StringTokenizer tokenizer = new StringTokenizer(text, delimiters);
    
    while (tokenizer.hasMoreTokens()) {
        tokens.add(tokenizer.nextToken());
    }
    
    return tokens;
}

// Using String split method
public static List<String> tokenizeWithSplit(String text, String delimiters) {
    // Escape special regex characters in delimiters
    String regex = "[" + Pattern.quote(delimiters) + "]";
    return Arrays.asList(text.split(regex));
}

// Examples
String text = "Hello,World;Java:Programming";

List<String> customTokens = customTokenize(text, ",;:");
// ["Hello", "World", "Java", "Programming"]

List<String> tokenizerTokens = tokenizeWithStringTokenizer(text, ",;:");
// ["Hello", "World", "Java", "Programming"]

List<String> splitTokens = tokenizeWithSplit(text, ",;:");
// ["Hello", "World", "Java", "Programming"]
```

### 27. How to encode and decode strings in different formats?
```java
// Base64 encoding/decoding
public static String encodeBase64(String text) {
    return Base64.getEncoder().encodeToString(text.getBytes());
}

public static String decodeBase64(String encoded) {
    byte[] decoded = Base64.getDecoder().decode(encoded);
    return new String(decoded);
}

// URL encoding/decoding
public static String encodeUrl(String url) throws UnsupportedEncodingException {
    return URLEncoder.encode(url, "UTF-8");
}

public static String decodeUrl(String encoded) throws UnsupportedEncodingException {
    return URLDecoder.decode(encoded, "UTF-8");
}

// HTML escape/unescape
public static String escapeHtml(String html) {
    return html.replace("&", "&amp;")
               .replace("<", "&lt;")
               .replace(">", "&gt;")
               .replace("\"", "&quot;")
               .replace("'", "&#39;");
}

public static String unescapeHtml(String escaped) {
    return escaped.replace("&amp;", "&")
                  .replace("&lt;", "<")
                  .replace("&gt;", ">")
                  .replace("&quot;", "\"")
                  .replace("&#39;", "'");
}

// Hexadecimal encoding/decoding
public static String encodeHex(String text) {
    StringBuilder hex = new StringBuilder();
    for (char c : text.toCharArray()) {
        hex.append(Integer.toHexString((int) c));
    }
    return hex.toString();
}

public static String decodeHex(String hex) {
    StringBuilder text = new StringBuilder();
    for (int i = 0; i < hex.length(); i += 2) {
        String str = hex.substring(i, i + 2);
        text.append((char) Integer.parseInt(str, 16));
    }
    return text.toString();
}

// Examples
String originalText = "Hello @World!";

String base64 = encodeBase64(originalText);
// "SGVsbG8gQFdvcmxkIQ=="
String fromBase64 = decodeBase64(base64);
// "Hello @World!"

String urlEncoded = encodeUrl(originalText);
// "Hello+%40World%21"
String urlDecoded = decodeUrl(urlEncoded);
// "Hello @World!"

String htmlEscaped = escapeHtml("<script>alert('XSS');</script>");
// "&lt;script&gt;alert(&#39;XSS&#39;);&lt;/script&gt;"
String htmlUnescaped = unescapeHtml(htmlEscaped);
// "<script>alert('XSS');</script>"
```

### 28. How to find the longest common substring between two strings?
```java
// Longest Common Substring using Dynamic Programming
public static String longestCommonSubstring(String str1, String str2) {
    if (str1 == null || str2 == null || str1.isEmpty() || str2.isEmpty()) {
        return "";
    }
    
    int m = str1.length();
    int n = str2.length();
    
    // Create a table to store lengths of common suffixes
    int[][] dp = new int[m + 1][n + 1];
    
    // Variables to keep track of the maximum length and ending position
    int maxLength = 0;
    int endIndex = 0;
    for (int i = 1; i <= m; i++) {
    for (int j = 1; j <= n; j++) {
    if (str1.charAt(i - 1) == str2.charAt(j - 1)) {
    dp[i][j] = dp[i - 1][j - 1] + 1;
    if (dp[i][j] > maxLength) {
    maxLength = dp[i][j];
    endIndex = i - 1;
    }
    }
    }
    }
    return str1.substring(endIndex - maxLength + 1, endIndex + 1);
    }
    // Example usage
    String s1 = "ABABC";
    String s2 = "BABCA";
    String lcs = longestCommonSubstring(s1, s2); // "BABC" or "ABC"
   

### 29. How to find the longest common subsequence between two strings?
```java
// Longest Common Subsequence using Dynamic Programming
public static String longestCommonSubsequence(String str1, String str2) {
    if (str1 == null || str2 == null || str1.isEmpty() || str2.isEmpty()) {
        return "";
    }
    
    int m = str1.length();
    int n = str2.length();
    
    // Create a table to store lengths of LCS
    int[][] dp = new int[m + 1][n + 1];
    
    // Fill the dp table
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (str1.charAt(i - 1) == str2.charAt(j - 1)) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }
    
    // Reconstruct the LCS from the dp table
    StringBuilder lcs = new StringBuilder();
    int i = m, j = n;
    
    while (i > 0 && j > 0) {
        if (str1.charAt(i - 1) == str2.charAt(j - 1)) {
            lcs.insert(0, str1.charAt(i - 1));
            i--;
            j--;
        } else if (dp[i - 1][j] > dp[i][j - 1]) {
            i--;
        } else {
            j--;
        }
    }
    
    return lcs.toString();
}

// Example usage
String s1 = "ABCBDAB";
String s2 = "BDCABA";
String lcs = longestCommonSubsequence(s1, s2);  // "BCBA" or "BDAB"
```

### 30. How to find the edit distance (Levenshtein distance) between two strings?
```java
// Edit Distance (Levenshtein distance) using Dynamic Programming
public static int editDistance(String word1, String word2) {
    int m = word1.length();
    int n = word2.length();
    
    // Create a table to store results of subproblems
    int[][] dp = new int[m + 1][n + 1];
    
    // Fill dp[][] in bottom-up manner
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            // If first string is empty, only option is to insert all characters of second string
            if (i == 0) {
                dp[i][j] = j;
            }
            // If second string is empty, only option is to remove all characters of first string
            else if (j == 0) {
                dp[i][j] = i;
            }
            // If last characters are the same, ignore the last char and recur for remaining
            else if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                dp[i][j] = dp[i - 1][j - 1];
            }
            // If last characters are different, consider all operations (insert, remove, replace)
            else {
                dp[i][j] = 1 + Math.min(Math.min(dp[i][j - 1],  // Insert
                                                dp[i - 1][j]),   // Remove
                                         dp[i - 1][j - 1]);      // Replace
            }
        }
    }
    
    return dp[m][n];
}

// Example usage
int distance1 = editDistance("kitten", "sitting");  // 3 (k→s, e→i, add g)
int distance2 = editDistance("sunday", "saturday");  // 3 (add 'a', add 't', add 'r')
```

### 31. How to check if two strings are anagrams of each other?
```java
// Check if two strings are anagrams
public static boolean areAnagrams(String str1, String str2) {
    if (str1 == null || str2 == null || str1.length() != str2.length()) {
        return false;
    }
    
    // Method 1: Using character frequency counting
    int[] counts = new int[256];  // Assuming ASCII characters
    
    for (int i = 0; i < str1.length(); i++) {
        counts[str1.charAt(i)]++;
        counts[str2.charAt(i)]--;
    }
    
    for (int count : counts) {
        if (count != 0) {
            return false;
        }
    }
    
    return true;
    
    /* Method 2: Using sorting
    char[] chars1 = str1.toCharArray();
    char[] chars2 = str2.toCharArray();
    
    Arrays.sort(chars1);
    Arrays.sort(chars2);
    
    return Arrays.equals(chars1, chars2);
    */
}

// Handling case-insensitive anagrams
public static boolean areAnagramsCaseInsensitive(String str1, String str2) {
    return areAnagrams(str1.toLowerCase(), str2.toLowerCase());
}

// Examples
boolean result1 = areAnagrams("listen", "silent");  // true
boolean result2 = areAnagrams("triangle", "integral");  // true
boolean result3 = areAnagrams("hello", "world");  // false
boolean result4 = areAnagramsCaseInsensitive("Race", "Care");  // true
```

### 32. How to find all anagrams of a string in another string?
```java
// Find all anagrams of pattern in text
public static List<Integer> findAnagrams(String text, String pattern) {
    List<Integer> result = new ArrayList<>();
    
    if (text == null || pattern == null || text.length() < pattern.length()) {
        return result;
    }
    
    int m = text.length();
    int n = pattern.length();
    
    // Character frequency arrays
    int[] patternFreq = new int[26];  // For lowercase alphabet
    int[] windowFreq = new int[26];
    
    // Calculate pattern frequency
    for (int i = 0; i < n; i++) {
        patternFreq[pattern.charAt(i) - 'a']++;
    }
    
    // Sliding window approach
    for (int i = 0; i < m; i++) {
        // Add current character to window
        windowFreq[text.charAt(i) - 'a']++;
        
        // Remove character that's now outside the window
        if (i >= n) {
            windowFreq[text.charAt(i - n) - 'a']--;
        }
        
        // Check if current window is an anagram of pattern
        if (i >= n - 1 && Arrays.equals(patternFreq, windowFreq)) {
            result.add(i - n + 1);  // Starting index of the anagram
        }
    }
    
    return result;
}

// Example
String text = "cbaebabacd";
String pattern = "abc";
List<Integer> indices = findAnagrams(text, pattern);  // [0, 6]
// "cba" at index 0 and "bac" at index 6 are anagrams of "abc"
```

### 33. How to compress a string in Java?
```java
// Basic run-length encoding
public static String compressString(String str) {
    if (str == null || str.isEmpty()) {
        return str;
    }
    
    StringBuilder compressed = new StringBuilder();
    char currentChar = str.charAt(0);
    int count = 1;
    
    for (int i = 1; i < str.length(); i++) {
        if (str.charAt(i) == currentChar) {
            count++;
        } else {
            compressed.append(currentChar);
            if (count > 1) {
                compressed.append(count);
            }
            
            currentChar = str.charAt(i);
            count = 1;
        }
    }
    
    // Don't forget the last set of characters
    compressed.append(currentChar);
    if (count > 1) {
        compressed.append(count);
    }
    
    String result = compressed.toString();
    
    // Return original string if compression didn't reduce size
    return result.length() < str.length() ? result : str;
}

// Using Java's built-in GZip compression
public static String gzipCompress(String str) throws IOException {
    if (str == null || str.isEmpty()) {
        return str;
    }
    
    ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
    try (GZIPOutputStream gzip = new GZIPOutputStream(outputStream)) {
        gzip.write(str.getBytes());
    }
    
    return Base64.getEncoder().encodeToString(outputStream.toByteArray());
}

public static String gzipDecompress(String compressed) throws IOException {
    if (compressed == null || compressed.isEmpty()) {
        return compressed;
    }
    
    byte[] bytes = Base64.getDecoder().decode(compressed);
    ByteArrayInputStream inputStream = new ByteArrayInputStream(bytes);
    
    StringBuilder result = new StringBuilder();
    try (GZIPInputStream gzipInputStream = new GZIPInputStream(inputStream);
         BufferedReader reader = new BufferedReader(new InputStreamReader(gzipInputStream))) {
        
        String line;
        while ((line = reader.readLine()) != null) {
            result.append(line);
        }
    }
    
    return result.toString();
}

// Examples
String original = "aaabbbcccddaaaa";
String compressed1 = compressString(original);  // "a3b3c3d2a4" or original if no benefit

String longText = "This is a long text that will be compressed using GZip compression algorithm...";
String compressed2 = gzipCompress(longText);
String decompressed = gzipDecompress(compressed2);  // Should equal longText
```

### 34. How to check if a string has all unique characters in Java?
```java
// Check for unique characters using a boolean array
public static boolean hasAllUniqueChars(String str) {
    if (str == null || str.isEmpty()) {
        return true;
    }
    
    // If string length exceeds number of unique characters possible
    if (str.length() > 128) {  // Assuming ASCII
        return false;
    }
    
    boolean[] charSet = new boolean[128];  // For ASCII
    
    for (int i = 0; i < str.length(); i++) {
        int val = str.charAt(i);
        
        // If the character is already found, return false
        if (charSet[val]) {
            return false;
        }
        
        charSet[val] = true;
    }
    
    return true;
}

// Using a Set for Unicode characters
public static boolean hasAllUniqueCharsSet(String str) {
    if (str == null || str.isEmpty()) {
        return true;
    }
    
    Set<Character> charSet = new HashSet<>();
    
    for (char c : str.toCharArray()) {
        if (!charSet.add(c)) {
            return false;
        }
    }
    
    return true;
}

// Without additional data structures (with sorting)
public static boolean hasAllUniqueCharsNoExtraDS(String str) {
    if (str == null || str.isEmpty()) {
        return true;
    }
    
    char[] chars = str.toCharArray();
    Arrays.sort(chars);
    
    for (int i = 0; i < chars.length - 1; i++) {
        if (chars[i] == chars[i + 1]) {
            return false;
        }
    }
    
    return true;
}

// Examples
boolean result1 = hasAllUniqueChars("abcdefg");  // true
boolean result2 = hasAllUniqueChars("hello");    // false (repeated 'l')
```

### 35. How to find the first non-repeated character in a string?
```java
// Find first non-repeating character using character frequency counting
public static char firstNonRepeatingChar(String str) {
    if (str == null || str.isEmpty()) {
        return '\0';  // Null character
    }
    
    // Count frequency of each character
    Map<Character, Integer> counts = new LinkedHashMap<>();  // Maintains insertion order
    
    for (char c : str.toCharArray()) {
        counts.put(c, counts.getOrDefault(c, 0) + 1);
    }
    
    // Find the first character with count 1
    for (Map.Entry<Character, Integer> entry : counts.entrySet()) {
        if (entry.getValue() == 1) {
            return entry.getKey();
        }
    }
    
    return '\0';  // No non-repeating character found
}

// More efficient single-pass approach (if we know we have ASCII)
public static char firstNonRepeatingCharEfficient(String str) {
    if (str == null || str.isEmpty()) {
        return '\0';
    }
    
    // Extended ASCII has 256 characters
    int[] count = new int[256];
    int[] index = new int[256];
    
    // Initialize index array
    Arrays.fill(index, -1);
    
    // Count occurrences and store first appearance
    for (int i = 0; i < str.length(); i++) {
        char c = str.charAt(i);
        if (count[c] == 0) {
            index[c] = i;
        }
        count[c]++;
    }
    
    int minIndex = Integer.MAX_VALUE;
    
    // Find the first non-repeating character
    for (int i = 0; i < 256; i++) {
        if (count[i] == 1 && index[i] < minIndex) {
            minIndex = index[i];
        }
    }
    
    return minIndex == Integer.MAX_VALUE ? '\0' : str.charAt(minIndex);
}

// Examples
char result1 = firstNonRepeatingChar("stress");  // 't'
char result2 = firstNonRepeatingChar("stream");  // 's'
char result3 = firstNonRepeatingChar("aabb");    // '\0' (no unique character)
```

### 36. How to check if a string is a rotation of another string?
```java
// Check if str2 is a rotation of str1
public static boolean isRotation(String str1, String str2) {
    if (str1 == null || str2 == null || str1.length() != str2.length() || str1.isEmpty()) {
        return false;
    }
    
    // Concat str1 with itself and check if str2 is a substring
    String concatenated = str1 + str1;
    return concatenated.contains(str2);
}

// Examples
boolean result1 = isRotation("waterbottle", "erbottlewat");  // true
boolean result2 = isRotation("abcde", "cdeab");             // true
boolean result3 = isRotation("abcde", "abced");             // false
```

### 37. How to find all the permutations of a string?
```java
// Generate all permutations of a string recursively
public static List<String> generatePermutations(String str) {
    List<String> permutations = new ArrayList<>();
    if (str == null) {
        return permutations;
    }
    
    if (str.length() == 0) {
        permutations.add("");
        return permutations;
    }
    
    char first = str.charAt(0);
    String remainder = str.substring(1);
    List<String> subPermutations = generatePermutations(remainder);
    
    for (String subPerm : subPermutations) {
        for (int i = 0; i <= subPerm.length(); i++) {
            String newPermutation = subPerm.substring(0, i) + first + subPerm.substring(i);
            permutations.add(newPermutation);
        }
    }
    
    return permutations;
}

// Generate unique permutations (handles duplicates)
public static List<String> generateUniquePermutations(String str) {
    List<String> result = new ArrayList<>();
    if (str == null) {
        return result;
    }
    
    char[] chars = str.toCharArray();
    Arrays.sort(chars);  // Sort to handle duplicates
    boolean[] used = new boolean[chars.length];
    StringBuilder current = new StringBuilder();
    
    generatePermutationsHelper(chars, used, current, result);
    
    return result;
}

private static void generatePermutationsHelper(char[] chars, boolean[] used, 
                                             StringBuilder current, List<String> result) {
    if (current.length() == chars.length) {
        result.add(current.toString());
        return;
    }
    
    for (int i = 0; i < chars.length; i++) {
        // Skip used characters or duplicates (when previous identical char is not used)
        if (used[i] || (i > 0 && chars[i] == chars[i - 1] && !used[i - 1])) {
            continue;
        }
        
        used[i] = true;
        current.append(chars[i]);
        
        generatePermutationsHelper(chars, used, current, result);
        
        used[i] = false;
        current.deleteCharAt(current.length() - 1);
    }
}

// Examples
List<String> permutations1 = generatePermutations("abc");
// ["abc", "bac", "bca", "acb", "cab", "cba"] (6 permutations)

List<String> permutations2 = generateUniquePermutations("abb");
// ["abb", "bab", "bba"] (3 unique permutations)
```

### 38. How to convert a string to an integer without using Integer.parseInt()?
```java
// Convert string to integer manually
public static int stringToInt(String str) throws NumberFormatException {
    if (str == null || str.isEmpty()) {
        throw new NumberFormatException("Empty or null string");
    }
    
    int result = 0;
    boolean isNegative = false;
    int i = 0;
    
    // Handle sign
    if (str.charAt(0) == '-' || str.charAt(0) == '+') {
        isNegative = str.charAt(0) == '-';
        i = 1;
    }
    
    // Process each digit
    for (; i < str.length(); i++) {
        char c = str.charAt(i);
        
        if (!Character.isDigit(c)) {
            throw new NumberFormatException("Invalid character: " + c);
        }
        
        int digit = c - '0';
        
        // Check for overflow
        if (result > Integer.MAX_VALUE / 10 || 
            (result == Integer.MAX_VALUE / 10 && digit > Integer.MAX_VALUE % 10)) {
            if (isNegative && result == Integer.MAX_VALUE / 10 && digit == 8) {
                return Integer.MIN_VALUE;  // Special case for MIN_VALUE
            }
            throw new NumberFormatException("Integer overflow");
        }
        
        result = result * 10 + digit;
    }
    
    return isNegative ? -result : result;
}

// Examples
int num1 = stringToInt("123");       // 123
int num2 = stringToInt("-456");      // -456
int num3 = stringToInt("+789");      // 789
// int num4 = stringToInt("12a34");  // Throws NumberFormatException
```

### 39. How to implement string interning?
```java
// Custom string interning using a pool of strings
public static class StringPool {
    private final Map<String, String> pool = new HashMap<>();
    
    public String intern(String str) {
        if (str == null) {
            return null;
        }
        
        // Return the pooled instance if it exists
        String existing = pool.get(str);
        if (existing != null) {
            return existing;
        }
        
        // Otherwise, add it to the pool and return it
        pool.put(str, str);
        return str;
    }
    
    public int size() {
        return pool.size();
    }
    
    public void clear() {
        pool.clear();
    }
}

// Examples of string interning
public static void demonstrateIntern() {
    // Java's built-in string interning
    String s1 = "hello";  // String literal goes to string pool
    String s2 = new String("hello");  // Creates a new object outside the pool
    String s3 = s2.intern();  // Returns the pooled instance
    
    System.out.println(s1 == s2);  // false (different objects)
    System.out.println(s1 == s3);  // true (same object from pool)
    System.out.println(s2 == s3);  // false (different objects)
    
    // Custom string interning
    StringPool customPool = new StringPool();
    String c1 = new String("world");
    String c2 = new String("world");
    
    // Intern both strings
    String ic1 = customPool.intern(c1);
    String ic2 = customPool.intern(c2);
    
    System.out.println(c1 == c2);   // false (different objects)
    System.out.println(ic1 == ic2); // true (same object from custom pool)
}
```

### 40. How to implement a custom string builder?
```java
// Simplified implementation of StringBuilder
public static class CustomStringBuilder {
    private char[] buffer;
    private int size;
    private static final int DEFAULT_CAPACITY = 16;
    
    public CustomStringBuilder() {
        buffer = new char[DEFAULT_CAPACITY];
        size = 0;
    }
    
    public CustomStringBuilder(String str) {
        this();
        if (str != null) {
            append(str);
        }
    }
    
    public CustomStringBuilder append(String str) {
        if (str == null) {
            return append("null");
        }
        
        int strLen = str.length();
        ensureCapacity(size + strLen);
        
        str.getChars(0, strLen, buffer, size);
        size += strLen;
        
        return this;
    }
    
    public CustomStringBuilder append(char c) {
        ensureCapacity(size + 1);
        buffer[size++] = c;
        return this;
    }
    
    public CustomStringBuilder insert(int offset, String str) {
        if (offset < 0 || offset > size) {
            throw new IndexOutOfBoundsException("Offset: " + offset);
        }
        
        if (str == null) {
            return insert(offset, "null");
        }
        
        int strLen = str.length();
        ensureCapacity(size + strLen);
        
        // Shift existing characters
        System.arraycopy(buffer, offset, buffer, offset + strLen, size - offset);
        
        // Copy new string at offset
        str.getChars(0, strLen, buffer, offset);
        size += strLen;
        
        return this;
    }
    
    public CustomStringBuilder delete(int start, int end) {
        if (start < 0 || start > size || start > end) {
            throw new IndexOutOfBoundsException("Start: " + start + ", End: " + end);
        }
        
        int len = Math.min(end, size) - start;
        if (len > 0) {
            System.arraycopy(buffer, start + len, buffer, start, size - start - len);
            size -= len;
        }
        
        return this;
    }
    
    public CustomStringBuilder reverse() {
        for (int i = 0; i < size / 2; i++) {
            char temp = buffer[i];
            buffer[i] = buffer[size - i - 1];
            buffer[size - i - 1] = temp;
        }
        
        return this;
    }
    
    public int length() {
        return size;
    }
    
    public char charAt(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index: " + index);
        }
        
        return buffer[index];
    }
    
    @Override
    public String toString() {
        return new String(buffer, 0, size);
    }
    
    private void ensureCapacity(int minCapacity) {
        if (minCapacity > buffer.length) {
            expandCapacity(minCapacity);
        }
    }
    
    private void expandCapacity(int minCapacity) {
        int newCapacity = Math.max(buffer.length * 2, minCapacity);
        char[] newBuffer = new char[newCapacity];
        System.arraycopy(buffer, 0, newBuffer, 0, size);
        buffer = newBuffer;
    }
}

// Example usage
public static void customStringBuilderExample() {
    CustomStringBuilder csb = new CustomStringBuilder();
    csb.append("Hello").append(' ').append("World!");
    System.out.println(csb.toString());  // "Hello World!"
    
    csb.insert(5, " Beautiful");
    System.out.println(csb.toString());  // "Hello Beautiful World!"
    
    csb.delete(6, 16);
    System.out.println(csb.toString());  // "Hello World!"
    
    csb.reverse();
    System.out.println(csb.toString());  // "!dlroW olleH"
}
```

## String Algorithms and Data Structures

### 41. How to implement a trie (prefix tree) for string storage and retrieval?
```java
// Trie implementation for efficient string operations
public static class Trie {
    private static class TrieNode {
        private final Map<Character, TrieNode> children = new HashMap<>();
        private boolean isEndOfWord;
        
        public Map<Character, TrieNode> getChildren() {
            return children;
        }
        
        public boolean isEndOfWord() {
            return isEndOfWord;
        }
        
        public void setEndOfWord(boolean endOfWord) {
            isEndOfWord = endOfWord;
        }
    }
    
    private final TrieNode root;
    
    public Trie() {
        root = new TrieNode();
    }
    
    // Insert a word into the trie
    public void insert(String word) {
        if (word == null || word.isEmpty()) {
            return;
        }
        
        TrieNode current = root;
        
        for (char c : word.toCharArray()) {
            TrieNode node = current.getChildren().get(c);
            if (node == null) {
                node = new TrieNode();
                current.getChildren().put(c, node);
            }
            current = node;
        }
        
        current.setEndOfWord(true);
    }
    
    // Search for a word in the trie
    public boolean search(String word) {
        if (word == null || word.isEmpty()) {
            return false;
        }
        
        TrieNode node = searchPrefix(word);
        return node != null && node.isEndOfWord();
    }
    
    // Check if any word in the trie starts with the given prefix
    public boolean startsWith(String prefix) {
        if (prefix == null || prefix.isEmpty()) {
            return false;
        }
        
        return searchPrefix(prefix) != null;
    }
    
    // Delete a word from the trie
    public void delete(String word) {
        delete(root, word, 0);
    }
    
    private boolean delete(TrieNode current, String word, int index) {
        if (index == word.length()) {
            if (!current.isEndOfWord()) {
                return false;
            }
            current.setEndOfWord(false);
            return current.getChildren().isEmpty();
        }
        
        char ch = word.charAt(index);
        TrieNode node = current.getChildren().get(ch);
        if (node == null) {
            return false;
        }
        
        boolean shouldDeleteCurrentNode = delete(node, word, index + 1) && !node.isEndOfWord();
        
        if (shouldDeleteCurrentNode) {
            current.getChildren().remove(ch);
            return current.getChildren().isEmpty();
        }
        
        return false;
    }
    
    // Find all words with the given prefix
    public List<String> findWordsWithPrefix(String prefix) {
        List<String> result = new ArrayList<>();
        TrieNode prefixNode = searchPrefix(prefix);
        
        if (prefixNode != null) {
            findAllWords(prefixNode, new StringBuilder(prefix), result);
        }
        
        return result;
    }
    
    private void findAllWords(TrieNode node, StringBuilder prefix, List<String> result) {
        if (node.isEndOfWord()) {
            result.add(prefix.toString());
        }
        
        for (Map.Entry<Character, TrieNode> child : node.getChildren().entrySet()) {
            char ch = child.getKey();
            TrieNode nextNode = child.getValue();
            
            prefix.append(ch);
            findAllWords(nextNode, prefix, result);
            prefix.deleteCharAt(prefix.length() - 1);
        }
    }
    
    private TrieNode searchPrefix(String word) {
        TrieNode current = root;
        
        for (char c : word.toCharArray()) {
            TrieNode node = current.getChildren().get(c);
            if (node == null) {
                return null;
            }
            current = node;
        }
        
        return current;
    }
}

// Example usage
public static void trieExample() {
    Trie trie = new Trie();
    trie.insert("apple");
    trie.insert("application");
    trie.insert("banana");
    trie.insert("app");
    
    System.out.println(trie.search("apple"));       // true
    System.out.println(trie.search("app"));         // true
    System.out.println(trie.search("appl"));        // false
    
    System.out.println(trie.startsWith("app"));     // true
    System.out.println(trie.startsWith("ban"));     // true
    System.out.println(trie.startsWith("cat"));     // false
    
    List<String> wordsWithApp = trie.findWordsWithPrefix("app");
    // ["app", "apple", "application"]
    
    trie.delete("apple");
    System.out.println(trie.search("apple"));       // false
    System.out.println(trie.search("application")); // true
}
```

### 42. How to implement the Rabin-Karp string matching algorithm?
```java
// Rabin-Karp string matching algorithm implementation
public static List<Integer> rabinKarp(String text, String pattern) {
    List<Integer> matches = new ArrayList<>();
    
    if (text == null || pattern == null || pattern.length() > text.length()) {
        return matches;
    }
    
    int n = text.length();
    int m = pattern.length();
    
    // Prime number for hash calculation
    int prime = 101;
    
    // Compute pattern hash and initial text window hash
    int patternHash = 0;
    int textHash = 0;
    int highestPower = 1;
    
    // Calculate hash for pattern and first window of text
    for (int i = 0; i < m; i++) {
        patternHash = (patternHash * 256 + pattern.charAt(i)) % prime;
        textHash = (textHash * 256 + text.charAt(i)) % prime;
        
        // Calculate 256^(m-1) for rolling hash
        if (i < m - 1) {
            highestPower = (highestPower * 256) % prime;
        }
    }
    
    // Slide pattern over text one by one
    for (int i = 0; i <= n - m; i++) {
        // Check hash equality and then verify with direct comparison
        if (patternHash == textHash) {
            boolean match = true;
            for (int j = 0; j < m; j++) {
                if (text.charAt(i + j) != pattern.charAt(j)) {
                    match = false;
                    break;
                }
            }
            
            if (match) {
                matches.add(i);
            }
        }
        
        // Calculate hash for next window
        if (i < n - m) {
            // Remove leading digit, add trailing digit, mod prime to avoid overflow
            textHash = (256 * (textHash - text.charAt(i) * highestPower) + text.charAt(i + m)) % prime;
            
            // Handle negative hash values
            if (textHash < 0) {
                textHash += prime;
            }
        }
    }
    
    return matches;
}

// Example usage
public static void rabinKarpExample() {
    String text = "ABABDABACDABABCABAB";
    String pattern = "ABABC";
    
    List<Integer> matches = rabinKarp(text, pattern);
    // Should contain [10] (match found at index 10)
    
    System.out.println("Pattern found at indices: " + matches);
}
```

### 43. How to implement the Knuth-Morris-Pratt (KMP) string matching algorithm?
```java
// Knuth-Morris-Pratt (KMP) string matching algorithm implementation
public static List<Integer> kmpSearch(String text, String pattern) {
    List<Integer> matches = new ArrayList<>();
    
    if (text == null || pattern == null || pattern.length() > text.length()) {
        return matches;
    }
    
    int[] lps = computeLPSArray(pattern);
    
    int i = 0;  // Index for text
    int j = 0;  // Index for pattern
    
    while (i < text.length()) {
        if (pattern.charAt(j) == text.charAt(i)) {
            i++;
            j++;
        }
        
        if (j == pattern.length()) {
            // Found a match
            matches.add(i - j);
            // Look for the next match
            j = lps[j - 1];
        } else if (i < text.length() && pattern.charAt(j) != text.charAt(i)) {
            if (j != 0) {
                j = lps[j - 1];
            } else {
                i++;
            }
        }
    }
    
    return matches;
}

// Compute the Longest Prefix Suffix (LPS) array for KMP
private static int[] computeLPSArray(String pattern) {
    int length = pattern.length();
    int[] lps = new int[length];
    
    int len = 0;  // Length of the previous longest prefix suffix
    int i = 1;
    
    while (i < length) {
        if (pattern.charAt(i) == pattern.charAt(len)) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                // Try to find a shorter prefix which is also a suffix
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
    
    return lps;
}

// Example usage
public static void kmpExample() {
    String text = "ABABDABACDABABCABAB";
    String pattern = "ABABC";
    
    List<Integer> matches = kmpSearch(text, pattern);
    // Should contain [10] (match found at index 10)
    
    System.out.println("Pattern found at indices: " + matches);
}
```

### 44. How to implement the Boyer-Moore string matching algorithm?
```java
// Boyer-Moore string matching algorithm implementation
public static List<Integer> boyerMoore(String text, String pattern) {
    List<Integer> matches = new ArrayList<>();
    
    if (text == null || pattern == null || pattern.isEmpty() || pattern.length() > text.length()) {
        return matches;
    }
    
    int n = text.length();
    int m = pattern.length();
    
    // Preprocessing: Last occurrence function
    Map<Character, Integer> lastOccurrence = new HashMap<>();
    for (int i = 0; i < m; i++) {
        lastOccurrence.put(pattern.charAt(i), i);
    }
    
    int i = m - 1;  // Start with the last character of the pattern
    int j = m - 1;
    
    while (i < n) {
        if (text.charAt(i) == pattern.charAt(j)) {
            if (j == 0) {
                // Found a match
                matches.add(i);
                i += m;  // Jump to the next potential match
                j = m - 1;
            } else {
                // Continue matching backwards
                i--;
                j--;
            }
        } else {
            // Character mismatch
            Integer lastPos = lastOccurrence.get(text.charAt(i));
            int badCharSkip = j - (lastPos != null ? lastPos : -1);
            
            i += Math.max(1, badCharSkip);  // Ensure at least one character shift
            j = m - 1;  // Reset pattern index to the end
        }
    }
    
    return matches;
}

// Example usage
public static void boyerMooreExample() {
    String text = "ABABDABACDABABCABAB";
    String pattern = "ABABC";
    List<Integer> matches = boyerMoore(text, pattern);
    // Should contain [10] (match found at index 10)
    System.out.println("Pattern found at indices: " + matches);
}


### 45. How to implement a suffix tree or suffix array for string matching?
```java
// Simplified suffix array implementation
public static class SuffixArray {
    private final String text;
    private final int[] suffixArray;
    
    public SuffixArray(String text) {
        this.text = text + "$"; // Add a sentinel character
        int n = this.text.length();
        
        // Create suffix array using simple sorting approach
        Integer[] indices = new Integer[n];
        for (int i = 0; i < n; i++) {
            indices[i] = i;
        }
        
        // Sort suffixes lexicographically
        Arrays.sort(indices, (a, b) -> this.text.substring(a).compareTo(this.text.substring(b)));
        
        // Convert to primitive array
        suffixArray = new int[n];
        for (int i = 0; i < n; i++) {
            suffixArray[i] = indices[i];
        }
    }
    
    // Find occurrences of a pattern using binary search
    public List<Integer> search(String pattern) {
        List<Integer> matches = new ArrayList<>();
        if (pattern == null || pattern.isEmpty()) {
            return matches;
        }
        
        int n = text.length();
        
        // Binary search for the starting position
        int left = 0;
        int right = n - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            String suffix = text.substring(suffixArray[mid]);
            
            int compare = pattern.compareTo(suffix.substring(0, Math.min(pattern.length(), suffix.length())));
            
            if (compare == 0) {
                // Found a match, collect all matches
                int i = mid;
                while (i >= 0 && isPrefix(pattern, suffixArray[i])) {
                    matches.add(suffixArray[i]);
                    i--;
                }
                
                i = mid + 1;
                while (i < n && isPrefix(pattern, suffixArray[i])) {
                    matches.add(suffixArray[i]);
                    i++;
                }
                
                break;
            } else if (compare < 0) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        
        return matches;
    }
    
    private boolean isPrefix(String pattern, int position) {
        String suffix = text.substring(position);
        if (suffix.length() < pattern.length()) {
            return false;
        }
        
        for (int i = 0; i < pattern.length(); i++) {
            if (pattern.charAt(i) != suffix.charAt(i)) {
                return false;
            }
        }
        
        return true;
    }
    
    // Print the suffix array
    public void printSuffixArray() {
        for (int i = 0; i < suffixArray.length; i++) {
            System.out.println(suffixArray[i] + ": " + text.substring(suffixArray[i]));
        }
    }
}

// Example usage
public static void suffixArrayExample() {
    String text = "banana";
    SuffixArray sa = new SuffixArray(text);
    
    sa.printSuffixArray();
    // Should print suffixes in sorted order:
    // 6: $
    // 5: a$
    // 3: ana$
    // 1: anana$
    // 0: banana$
    // 4: na$
    // 2: nana$
    
    List<Integer> matches = sa.search("ana");
    // Should contain [1, 3] (matches at positions 1 and 3)
    
    System.out.println("Pattern found at indices: " + matches);
}
```

### 46. How to implement text segmentation using dynamic programming?
```java
// Word break problem - determine if a string can be segmented into dictionary words
public static boolean wordBreak(String s, Set<String> wordDict) {
    if (s == null || s.isEmpty()) {
        return true;
    }
    
    int n = s.length();
    boolean[] dp = new boolean[n + 1];
    dp[0] = true;  // Empty string can be segmented
    
    // Maximum word length for optimization
    int maxWordLength = 0;
    for (String word : wordDict) {
        maxWordLength = Math.max(maxWordLength, word.length());
    }
    
    for (int i = 1; i <= n; i++) {
        // Check all possible word endings
        for (int j = i - 1; j >= 0 && j >= i - maxWordLength; j--) {
            if (dp[j] && wordDict.contains(s.substring(j, i))) {
                dp[i] = true;
                break;
            }
        }
    }
    
    return dp[n];
}

// Find all possible word break combinations
public static List<String> wordBreakAll(String s, Set<String> wordDict) {
    return wordBreakHelper(s, wordDict, new HashMap<>());
}

private static List<String> wordBreakHelper(String s, Set<String> wordDict, Map<String, List<String>> memo) {
    if (memo.containsKey(s)) {
        return memo.get(s);
    }
    
    List<String> result = new ArrayList<>();
    
    if (s.isEmpty()) {
        result.add("");
        return result;
    }
    
    for (String word : wordDict) {
        if (s.startsWith(word)) {
            String remaining = s.substring(word.length());
            List<String> subResults = wordBreakHelper(remaining, wordDict, memo);
            
            for (String subResult : subResults) {
                String space = subResult.isEmpty() ? "" : " ";
                result.add(word + space + subResult);
            }
        }
    }
    
    memo.put(s, result);
    return result;
}

// Example usage
public static void wordBreakExample() {
    Set<String> dictionary = new HashSet<>(Arrays.asList("cat", "cats", "and", "sand", "dog"));
    
    boolean canBreak1 = wordBreak("catsanddog", dictionary);
    System.out.println("Can break 'catsanddog': " + canBreak1);  // true
    
    boolean canBreak2 = wordBreak("catsanddogs", dictionary);
    System.out.println("Can break 'catsanddogs': " + canBreak2);  // false
    
    List<String> allBreaks = wordBreakAll("catsanddog", dictionary);
    // Should contain ["cat sand dog", "cats and dog"]
    System.out.println("All possible word breaks: " + allBreaks);
}
```

### 47. How to detect and correct spelling errors using the Levenshtein distance?
```java
// Calculate Levenshtein (edit) distance between two strings
public static int levenshteinDistance(String s1, String s2) {
    if (s1 == null || s2 == null) {
        return s1 == null ? (s2 == null ? 0 : s2.length()) : s1.length();
    }
    
    int m = s1.length();
    int n = s2.length();
    
    // Base cases: empty strings
    if (m == 0) return n;
    if (n == 0) return m;
    
    // Use a single array to save space
    int[] previousRow = new int[n + 1];
    int[] currentRow = new int[n + 1];
    
    // Initialize the first row
    for (int j = 0; j <= n; j++) {
        previousRow[j] = j;
    }
    
    for (int i = 1; i <= m; i++) {
        currentRow[0] = i;
        
        for (int j = 1; j <= n; j++) {
            int insertCost = currentRow[j - 1] + 1;
            int deleteCost = previousRow[j] + 1;
            
            int replaceCost;
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                replaceCost = previousRow[j - 1];  // No cost for matching characters
            } else {
                replaceCost = previousRow[j - 1] + 1;
            }
            
            currentRow[j] = Math.min(Math.min(insertCost, deleteCost), replaceCost);
        }
        
        // Swap arrays for next iteration
        int[] temp = previousRow;
        previousRow = currentRow;
        currentRow = temp;
    }
    
    return previousRow[n];
}

// Spell check using Levenshtein distance
public static List<String> spellCheck(String word, Set<String> dictionary, int maxDistance) {
    List<String> suggestions = new ArrayList<>();
    
    for (String dictWord : dictionary) {
        int distance = levenshteinDistance(word, dictWord);
        if (distance <= maxDistance) {
            suggestions.add(dictWord);
        }
    }
    
    // Sort by distance (closest matches first)
    suggestions.sort((w1, w2) -> Integer.compare(
        levenshteinDistance(word, w1), 
        levenshteinDistance(word, w2)
    ));
    
    return suggestions;
}

// Example usage
public static void spellCheckExample() {
    Set<String> dictionary = new HashSet<>(Arrays.asList(
        "hello", "world", "programming", "java", "algorithm", "computer", "keyboard"
    ));
    
    String misspelled = "helo";
    List<String> suggestions = spellCheck(misspelled, dictionary, 2);
    // Should contain ["hello"]
    
    System.out.println("Suggestions for '" + misspelled + "': " + suggestions);
    
    misspelled = "progaming";
    suggestions = spellCheck(misspelled, dictionary, 3);
    // Should contain ["programming"]
    
    System.out.println("Suggestions for '" + misspelled + "': " + suggestions);
}
```

### 48. How to implement autocomplete functionality?
```java
// Autocomplete implementation using a Trie
public static class Autocomplete {
    private final Trie trie;
    
    public Autocomplete() {
        trie = new Trie();
    }
    
    // Add words to the autocomplete dictionary
    public void addWords(List<String> words) {
        for (String word : words) {
            trie.insert(word);
        }
    }
    
    // Get autocomplete suggestions for a prefix
    public List<String> getSuggestions(String prefix, int limit) {
        List<String> allMatches = trie.findWordsWithPrefix(prefix);
        
        // Limit the number of suggestions
        return allMatches.size() <= limit ? 
               allMatches : 
               allMatches.subList(0, limit);
    }
    
    // Get suggestions with custom ranking (e.g., by frequency)
    public List<String> getSuggestionsRanked(String prefix, Map<String, Integer> wordFrequency, int limit) {
        List<String> matches = trie.findWordsWithPrefix(prefix);
        
        // Sort by frequency (descending)
        matches.sort((w1, w2) -> Integer.compare(
            wordFrequency.getOrDefault(w2, 0),
            wordFrequency.getOrDefault(w1, 0)
        ));
        
        // Limit the number of suggestions
        return matches.size() <= limit ? 
               matches : 
               matches.subList(0, limit);
    }
}

// Example usage
public static void autocompleteExample() {
    Autocomplete ac = new Autocomplete();
    
    List<String> dictionary = Arrays.asList(
        "apple", "application", "app", "apartment", "appear", "ball", "banana", "batman", "battle"
    );
    
    ac.addWords(dictionary);
    
    List<String> suggestions1 = ac.getSuggestions("app", 3);
    // Should contain ["app", "apple", "application"]
    System.out.println("Suggestions for 'app': " + suggestions1);
    
    List<String> suggestions2 = ac.getSuggestions("ba", 3);
    // Should contain ["ball", "banana", "batman"]
    System.out.println("Suggestions for 'ba': " + suggestions2);
    
    // With frequency ranking
    Map<String, Integer> wordFrequency = new HashMap<>();
    wordFrequency.put("application", 100);
    wordFrequency.put("apple", 75);
    wordFrequency.put("app", 50);
    wordFrequency.put("apartment", 25);
    
    List<String> rankedSuggestions = ac.getSuggestionsRanked("ap", wordFrequency, 3);
    // Should contain ["application", "apple", "app"] (sorted by frequency)
    System.out.println("Ranked suggestions for 'ap': " + rankedSuggestions);
}
```

### 49. How to implement a string interning with a WeakHashMap?
```java
// String interning with a WeakHashMap
public static class WeakStringPool {
    private final Map<String, WeakReference<String>> pool = new WeakHashMap<>();
    
    public String intern(String str) {
        if (str == null) {
            return null;
        }
        
        WeakReference<String> ref = pool.get(str);
        String existingString = ref != null ? ref.get() : null;
        
        if (existingString != null) {
            return existingString;
        }
        
        pool.put(str, new WeakReference<>(str));
        return str;
    }
    
    public int size() {
        return pool.size();
    }
    
    public void cleanup() {
        System.gc();  // Suggest garbage collection to clean up weak references
    }
}

// Example usage
public static void weakStringPoolExample() {
    WeakStringPool pool = new WeakStringPool();
    
    String s1 = new String("hello");
    String s2 = new String("hello");
    
    String interned1 = pool.intern(s1);
    String interned2 = pool.intern(s2);
    
    System.out.println("Original strings same object: " + (s1 == s2));  // false
    System.out.println("Interned strings same object: " + (interned1 == interned2));  // true
    
    System.out.println("Pool size: " + pool.size());  // 1
    
    // Let's make the string eligible for garbage collection
    s1 = null;
    s2 = null;
    interned1 = null;
    interned2 = null;
    
    pool.cleanup();
    
    // After garbage collection, weak references should be cleared
    System.out.println("Pool size after cleanup: " + pool.size());  // May be 0 after GC
}
```

### 50. How to implement string compression and decompression?
```java
// Advanced string compression using run-length encoding with handling for special cases
public static class StringCompressor {
    // Compress a string using run-length encoding
    public static String compress(String input) {
        if (input == null || input.length() <= 1) {
            return input;
        }
        
        StringBuilder compressed = new StringBuilder();
        char currentChar = input.charAt(0);
        int count = 1;
        
        for (int i = 1; i < input.length(); i++) {
            if (input.charAt(i) == currentChar) {
                count++;
            } else {
                appendCompressedChar(compressed, currentChar, count);
                currentChar = input.charAt(i);
                count = 1;
            }
        }
        
        // Don't forget the last set of characters
        appendCompressedChar(compressed, currentChar, count);
        
        // Return original string if compression didn't help
        return compressed.length() < input.length() ? compressed.toString() : input;
    }
    
    // Helper method to append compressed character and count
    private static void appendCompressedChar(StringBuilder sb, char c, int count) {
        sb.append(c);
        if (count > 1) {
            sb.append(count);
        }
    }
    
    // Decompress a run-length encoded string
    public static String decompress(String compressed) {
        if (compressed == null || compressed.isEmpty()) {
            return compressed;
        }
        
        StringBuilder decompressed = new StringBuilder();
        
        int i = 0;
        while (i < compressed.length()) {
            char c = compressed.charAt(i++);
            
            // Find the count (may be multiple digits)
            int count = 1;
            StringBuilder countStr = new StringBuilder();
            
            while (i < compressed.length() && Character.isDigit(compressed.charAt(i))) {
                countStr.append(compressed.charAt(i++));
            }
            
            if (countStr.length() > 0) {
                count = Integer.parseInt(countStr.toString());
            }
            
            // Append the character 'count' times
            for (int j = 0; j < count; j++) {
                decompressed.append(c);
            }
        }
        
        return decompressed.toString();
    }
    
    // Compress using dictionary-based approach (simplified LZW)
    public static String compressLZW(String input) {
        if (input == null || input.length() <= 1) {
            return input;
        }
        
        Map<String, Integer> dictionary = new HashMap<>();
        
        // Initialize dictionary with single characters
        for (int i = 0; i < 256; i++) {
            dictionary.put(String.valueOf((char)i), i);
        }
        
        String current = "";
        StringBuilder compressed = new StringBuilder();
        
        for (char c : input.toCharArray()) {
            String combined = current + c;
            
            if (dictionary.containsKey(combined)) {
                current = combined;
            } else {
                compressed.append(dictionary.get(current)).append(" ");
                dictionary.put(combined, dictionary.size());
                current = String.valueOf(c);
            }
        }
        
        // Output the last code
        if (!current.isEmpty()) {
            compressed.append(dictionary.get(current));
        }
        
        return compressed.toString();
    }
}

// Example usage
public static void compressionExample() {
    String original = "aabcccccaaa";
    String compressed = StringCompressor.compress(original);
    System.out.println("Original: " + original);
    System.out.println("Compressed: " + compressed);  // "a2bc5a3"
    
    String decompressed = StringCompressor.decompress(compressed);
    System.out.println("Decompressed: " + decompressed);  // Should equal original
    
    String originalLong = "ABABABABABABABABABABABABABABABABABABABA";
    String compressedLZW = StringCompressor.compressLZW(originalLong);
    System.out.println("LZW compressed: " + compressedLZW);
}
```

