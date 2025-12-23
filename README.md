# Two-Best-Non-Overlapping-Events

You are given a 0-indexed 2D integer array of events where events[i] = [startTimei, endTimei, valuei]. The ith event starts at startTimei and ends at endTimei, and if you attend this event, you will receive a value of valuei. You can choose at most two non-overlapping events to attend such that the sum of their values is maximized.

Return this maximum sum.

Note that the start time and end time is inclusive: that is, you cannot attend two events where one of them starts and the other ends at the same time. More specifically, if you attend an event with end time t, the next event must start at or after t + 1.

class Solution:
    def maxTwoEvents(self, events: List[List[int]]) -> int:

        end_sorted = deque(sorted(events, key=itemgetter(1)))
        start_sorted = sorted(events, key=itemgetter(0))

        ans = max(v for _, _, v in events)

        end_max = 0  

        for start, end, value in start_sorted:
            while end_sorted and end_sorted[0][1] < start:
                _, _, v = end_sorted.popleft()
                end_max = max(end_max, v)
            ans = max(ans, value + end_max)

        return ans
