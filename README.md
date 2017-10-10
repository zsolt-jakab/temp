import java.util.Deque;
import java.util.LinkedList;
import java.util.Scanner;

public class Solution {

    private static class Element {

        private final long sum;

        private final int count;

        public Element(long sum, int count) {
            this.sum = sum;
            this.count = count;
        }
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        int g = in.nextInt();
        for (int a0 = 0; a0 < g; a0++) {
            int n = in.nextInt();
            int m = in.nextInt();
            int x = in.nextInt();

            Deque<Element> a = new LinkedList<>();

            long sum = 0;
            for (int i = 0; i < n; i++) {
                int value = in.nextInt();
                sum += value;
                int count = i + 1;
                if(sum <= x) {
                    a.addLast(new Element(sum, count));
                }
            }

            Deque<Element> b = new LinkedList<>();

            sum = 0;
            for (int i = 0; i < m; i++) {
                int value = in.nextInt();
                sum += value;
                int count = i + 1;
                if(sum <= x) {
                    b.addLast(new Element(sum, count));
                }
            }

            System.out.println(maxScore(a, b, x));

        }
    }

    private static long maxScore(Deque<Element> a, Deque<Element> b, int x) {
        long max = a.isEmpty() ? 0 : a.getLast().count;
        while(!a.isEmpty()) {
            Element elementA = a.removeLast();
            while (!b.isEmpty() && b.getFirst().sum + elementA.sum <=  x) {
                Element elementB = b.removeFirst();
                if(max < elementA.count + elementB.count) {
                    max = elementA.count + elementB.count;
                }
            }
        }
        if(!b.isEmpty()) {
            max = max < b.getLast().count ? b.getLast().count : max;
        }

        return max;
    }
}
