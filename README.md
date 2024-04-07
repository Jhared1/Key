import android.content.Context;
import java.io.FileOutputStream;
import java.io.IOException;
import java.security.SecureRandom;
import java.math.BigInteger;

public class KeyGenerator {

    // Method to generate a random key of specified length
    public static String generateRandomKey(int length) {
        SecureRandom secureRandom = new SecureRandom();
        byte[] bytes = new byte[length];
        secureRandom.nextBytes(bytes);
        BigInteger bigInt = new BigInteger(1, bytes);
        // Convert the random bytes into a hexadecimal string
        String key = bigInt.toString(16);
        // Pad the string with zeros if necessary
        while (key.length() < length * 2) {
            key = "0" + key;
        }
        return key;
    }

    // Method to write the generated key to a file in internal storage
    public static void writeKeyToFile(Context context, String key, String filename) {
        try {
            FileOutputStream fos = context.openFileOutput(filename, Context.MODE_PRIVATE);
            fos.write(key.getBytes());
            fos.close();
            System.out.println("Key written to " + filename);
        } catch (IOException e) {
            System.err.println("Error writing key to file: " + e.getMessage());
        }
    }
}
