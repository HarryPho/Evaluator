package assignment3;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

import junit.framework.TestCase;

@SuppressWarnings("unchecked")
public class EvaluatorTest extends TestCase {

    private Evaluator evaluator;

    protected void setUp() {
        evaluator = new Evaluator();
    }

    public void testCanary() {
        assertTrue(true);
    }

    private HashMap<String, String> creditEvaluateApproved(String SSN) {
        HashMap<String, String> result = new HashMap<>();
        result.put("checkStatus", "Approved");
        result.put("reason", "Good Credit");
        return result;
    }

    private HashMap<String, String> creditEvaluateRejected(String SSN) {
        HashMap<String, String> result = new HashMap<>();
        result.put("checkStatus", "Rejected");
        result.put("reason", "Bad Credit");
        return result;
    }

    private HashMap<String, String> criminalEvaluateApproved(String SSN) {
        HashMap<String, String> result = new HashMap<>();
        result.put("checkStatus", "Approved");
        result.put("reason", "No Criminal");
        return result;
    }

    private HashMap<String, String> criminalEvaluateRejected(String SSN) {
        HashMap<String, String> result = new HashMap<>();
        result.put("checkStatus", "Rejected");
        result.put("reason", "Criminal Record");
        return result;
    }

    public Map<String, Object> createMapFor(String SSN, String firstName, String lastName, String status, String... reasons) {
        Map<String, Object> expectedResult = new HashMap<>();
        expectedResult.put("SSN", SSN);
        expectedResult.put("firstName", firstName);
        expectedResult.put("lastName", lastName);
        expectedResult.put("checkStatus", status);
        expectedResult.put("reason", Arrays.asList(reasons));

        return expectedResult;
    }

    public void testCreditApproved() {
        Map<String, Object> expectedResult = createMapFor("123456789", "John", "Doe", "Approved", "Good Credit");
        assertEquals(expectedResult, evaluator.evaluate("123456789", "John", "Doe", this::creditEvaluateApproved));
    }

    public void testCreditRejection() {
        Map<String, Object> expectedResult = createMapFor("684772647", "Katy", "Perry", "Rejected", "Bad Credit");
        assertEquals(expectedResult, evaluator.evaluate("684772647", "Katy", "Perry", this::creditEvaluateRejected));
    }

    public void testIsCriminal() {
        Map<String, Object> expectedResult = createMapFor("112233445", "John", "Doe", "Approved", "No Criminal");
        assertEquals(expectedResult, evaluator.evaluate("112233445", "John", "Doe", this::criminalEvaluateApproved));
    }

    public void testIsNotCriminal() {
        Map<String, Object> expectedResult = createMapFor("112233445", "John", "Doe", "Rejected", "Criminal Record");
        assertEquals(expectedResult, evaluator.evaluate("112233445", "John", "Doe", this::criminalEvaluateRejected));
    }

    public void testApproveTwoCriteria() {
        Map<String, Object> expectedResult = createMapFor("123456789", "John", "Doe", "Approved", "Good Credit", "No Criminal");
        assertEquals(expectedResult, evaluator.evaluate("123456789", "John", "Doe", this::creditEvaluateApproved, this::criminalEvaluateApproved));
    }

    public void testRejectTwoCriteria() {
        Map<String, Object> expectedResult = createMapFor("123456789", "John", "Doe", "Rejected", "Bad Credit", "Criminal Record");
        assertEquals(expectedResult, evaluator.evaluate("123456789", "John", "Doe", this::creditEvaluateRejected, this::criminalEvaluateRejected));
    }

    public void testApproveFirstRejectSecondCriteria() {
        Map<String, Object> expectedResult = createMapFor("123456789", "John", "Doe", "Rejected", "Good Credit", "Criminal Record");
        assertEquals(expectedResult, evaluator.evaluate("123456789", "John", "Doe", this::creditEvaluateApproved, this::criminalEvaluateRejected));
    }

    public void testApproveSecondRejectFirstCriteria() {
        Map<String, Object> expectedResult = createMapFor("123456789", "John", "Doe", "Rejected", "Bad Credit", "No Criminal");
        assertEquals(expectedResult, evaluator.evaluate("123456789", "John", "Doe", this::creditEvaluateRejected, this::criminalEvaluateApproved));
    }

    public void testNoCriteriaCriteriaa() {
        try {
            evaluator.evaluate("123456789", "John", "Doe");
            fail("Expected test to fail when no background check service was provided");
        } catch (RuntimeException rte) {
        }
    }
}