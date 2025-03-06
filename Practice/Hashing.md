```
import java.util.*;

public class Main {
    public static int[] twoSum(int[] arr, int target) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < arr.length - 1; i++) {
            int diff = target - arr[i];
            if (map.containsKey(diff)) {
                return new int[]{map.get(diff), i};
            }
            map.put(arr[i], i);
        }
        System.out.println(map);
        return new int[]{};
    }

    public static List<List<String>> groupAnagrams(String[] words) {
        Map<String, List<String>> map = new HashMap<>();
        for (String word : words) {
            char[] chars = word.toCharArray();
            Arrays.sort(chars);
            String sorted = new String(chars);
            map.putIfAbsent(sorted, new ArrayList<>());
            map.get(sorted).add(word);
        }

        return new ArrayList<>(map.values());
    }

    public static void main(String[] args) {
        int[] arr = {2, 7, 11, 15};
        int target = 45;
        int[] result = twoSum(arr, target);
        System.out.println(Arrays.toString(result));

        String[] words = { "eat", "tea", "tan", "ate", "nat", "bat" };
        System.out.println(groupAnagrams(words));
    }
}

```
