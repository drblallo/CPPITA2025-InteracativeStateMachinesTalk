# Interactive Program Design in C++: Snippets

---

## Running example

[godbolt](https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGEs6SuADJ4DJgAcj4ARpjEIGYBAA6oCoRODB7evv6kyamOAiFhkSwxcQm2mPYFDEIETMQEmT5%2BXAF2mA7pdQ0ERRHRsfHt9Y3N2W22o32hA6VDCQCUtqhexMjsHOYAzKHI3lgA1Cbbbk4KBMSYrCfYJhoAgjt7B5jHp8SG6Kgst/dPZl2DH2XiOJzcYmAJEICF%2B2zuj3%2BoQIh2InloABUAO6oAAieA2EEWxwA7FZHodKYcLkxHMhqQR0CAQJ8GN8WAB9LAANwJb2I6BO5IeVIZtIJDKZIBYBC4AE45dsSYdgIwIAKiYshf9RRcpV4GHh%2BMROciuXgLsQ8FEvDVwcjbod0BAuKRDgA2LXbYWiq4ENYMJ3QRjE6xB1UML3Ckwk3H/f5RVCeQ5eJTEADqhgICgxqAASrF0UTST6qXrmWhbe83ODjgkCwovLQUbWSQA6Q4FtG0WgnABixwArBYAJ4AegYJkHuLrZm1FLLjOZltCwGp85FVKNhwgYEg5ZQoXed3h1MWxL9AcOVDESg3vsw/uIgb3CjbmBYiQII%2BL5ndf53BQpwsDQpzjbZwNxMAOBHaDSRrEk3HXYdQOnE5IOggBNaCo3jWN40eZEUzTXFOjwLB0AARS8LNCB/UMyR1RcpUrFtTlrcwzAedB0EOJhDgYQZiEOGICCxTBGEODQ%2BLZQ5BxAWd7y3QRDgAR3eGdQO9JjKW3Xd9yXQ9Az%2BU9VPPVFHyvLTS0pS9n0lCsDE/CBVLdDQ3UHXDEXwxFHm5VByNRA1DSMbBVFYRJ6F/RiF10lSrkbZsNNRdFsTxPkiSUykD1Y6sOISPs8GIC4Up7BTOLy04LMStiayqzipzcScEg3HTDj0hKm1qw5lT/ADU1iTNBBzfNCx7TUSzah8auS7tMRxfFCS8zdRWywzcvBfKzC7dFMCZWdKqQzqks2%2BqWsHJqGu02LVpy1Zaq2wrmFoaquvKhJDtek72LOucLuaudrpW1a7MnIHRRjONfOB46W0sdDiNiUjkHIvbqNo79MvB5iK3uz7OKesQvoId6zE%2B2H8fOy6WqByGCIeIiWCYUJopsoKGBC4AwoiqLlrpx4OGWWhOEHXg/A4LRSFQTga3hyxqVWdY3h2HhSBJiXBeWABrEBtm2Ns9cNo3jfdfROEkMXNF4aWOF4BQQHc9WtGWOBYCQNBPzoWJyEoD3Ei9uJgC4QcAhoZtYntiAoit0golCBoR04VW4%2BYYgRwAeSibROnV1WPbYQR04YWhE410gsBtYAIR7e3uF4LAmaMcQy/wK4um5TBa8lzBVE6W1Nkl5Eqhj2hrU%2BNOPCwGPLjwFgk94DviETJRSMb4BR6MK3lioAxgAUAA1PBMCxdPEkYeeZEEEQxHYKRL/kJQ1Bj3RXQMTfTDlmxR6ie3IGWVAvzpFrtbReVosC/yJJUao6QXBsnGH4OUgQ2T9BKGUeIJJXR5DSAIeBIBEFYJqCgoS6DXQdC6AIHoYxPAtDwVAnO3RphEPmOUDBUxei4MQTSRoTC0FmAwcsBQisNgSCFiLS2ZcbaHFUAADndAAWndJIFUyB6TBzbGTCAuBCAkDrNsLgixeBO01qQHWesDbGwsXrU2wsOAW1IOLSWNs7YOzVlvUgrtEAgHuokW0PsIB%2BwDuEVgmwZHyMUco1Rg51G8D2tosBeh%2BBX1EOIO%2BiSH4qHUGXF%2BpAsSfESPPURHBRb2JjjbdOtofEolQFQKRsiFFKOACow4aiNEeE9vQYSKsDGuI1ueExut9aWMsWbWx4jHGcGcY7LehSzBjOthMnpztliL1SM4SQQA%3D)
```cpp
#include <iostream>
#include <random>
#include <algorithm>

int rollTwoDice() {
    static std::random_device rd;
    static std::mt19937 gen(rd());
    std::uniform_int_distribution<int> d(1, 6);
    return d(gen) + d(gen);
}

bool userWantsToReroll() {
    std::cout << "Result < 7. Reroll? [y/n] ";
    std::string s;
    if (!(std::cin >> s)) return false;
    return !s.empty() && (s[0]=='y' || s[0]=='Y');
}

int userDecidedQuantity() {
    std::cout << "Add a number between 0 and 5: ";
    int q = 0;
    if (!(std::cin >> q)) return 0;
    return std::clamp(q, 0, 5);
}

void runningExample() {
    int result = rollTwoDice();
    std::cout << "First roll: " << result << "\n";

    if (result < 7 && userWantsToReroll()) {
        result = rollTwoDice();
        std::cout << "Rerolled: " << result << "\n";
        std::cout << "Final result: " << result << "\n";
        return;
    }

    result += userDecidedQuantity();
    std::cout << "Final result: " << result << "\n";
}

int main() {
    runningExample();
}
```
* Straight, **blocking** control flow: user input pauses the thread.
* Clear , but unsuitable when a **framework owns the main loop** (engines/servers) or when you need to **stop/serialize/restore** the execution.

---

## Intuitive running example class rewrite
[godbolt](https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGIAKxmpK4AMngMmAByPgBGmMQgkgAcpAAOqAqETgwe3r566ZmOAmER0SxxCcm2mPbFDEIETMQEuT5%2BgTV12Y3NBKVRsfGJKQpNLW35XLbj/eGDFcPJAJS2qF7EyOwc5gDM4cjeWADUJrtuTmPEmKxn2CYaAIJ7B0eYp%2BfEhuioLHcPzzM%2BwYhy8JzObjEwBIhAQf129yeLxBbw%2BblECiULX%2BSKe4QIx2InloABUAO6oAAieC2EGWpwA7FYnsdWccxkxHMh2QR0CAQF8GD8WAB9LAANxp72I6DOFh5nJpPL5IBYBC4AE4NbsGcdgIwIDK6cs5QC2cr%2BV4GHh%2BMRRfixXgrngYl56hD8XdjugINMAGwm3bMx7m64EDYMb3QRj06xR/UMQPBkwMykAgFXLwOY4AJSt1qM2FUrFS9EZwfNjB8x0imFUBJT8t6LQ%2BlOOGlIxwA6kxCDn4sTOz3CABFLyGRwEACencpAneKbTQbNbNr9eOEXXZzbzYIppZbPxrOuCi8tAbuzbGn3zwPrPFqDw6AVLTp5ZX5tZTEx8QIEE3F5LjusxJh%2Bn4nmegGEsS5JUlKdI3p%2BbJjCqaBumiEKnGYZgAGJ4MQYzQbQtAgFhZgYechKYKe54UW4ZEmP4bgMOYZiIUhG51lBhrUZBaLHAysa7Dh3a9gQ/ZEsRxykcOBBjhOhBTuxrKLumd7HA%2BT7HF4WIScSCgQDEqCeMchBiqg1GxkyYHmt%2BWJ/gBrbbqJfYDsRoHqeaNrHBAZk/JZ76eRxEG0c5kmkhS1K0h5IYceaKH8mhF5uJhrF6cRmB8mRdFUTRyWpdhjHMaxylxZxW6Xscc4RKV5qLsctRKIFsVleVUGyfJgiKbVbKqepfW3i1GmPs%2BOnxJSmDIE%2B1GdZOU6%2BYIxwAI5WRWHF2b%2B/5cU5lUdeOXXTjFcUhQ2ljOQlKAGCwqQQEtnYdsc/hHRxjnOdVmClQNYFGSZTrmREb5oAwhGNlR4bEJGr2Xm985yoyaZIqmN4AkeLC9gwb6NmBeYMAWwBFiWZYKPCa2ssTAB0HKvs9rLeRAFNQ0Bub5uE%2BPFtd4ggLJ6W0PSFNjcQPMGVQYhKDTplUD5DPbduzk43jBMc%2BwXNibNil8yw5MCxNU1YAoavThAuzi3TFN/T8APLHzvKJes%2BWUaxeHMLQuWQaRrE5RTJ05SVTEsYVy6Iwjg0cKsJEcP4vB%2BBwWikKgnApWdljsusmwLkCPCkAQmih6sADWIC7Ls5NF6XZfl36%2BicJIUc53HnC8AoIAdtnMeh6QcCwEgaDXXQ8TkJQPepH3CTAFwnQ0Oe8RN4ZdcxOEzRTpwmfz8wxBTgA8jE2iTa3mc92wggbwwtBL23pBYK6wCQsRTfcLwWBo0Y4jn/g1wOHg4rUXXdaTW62yx3xLUOutAXRfHXh4LAdcCDEDwCwZevAv7ECMkoCaT9gCgKMDnVYVADDAAUAANTwJgMkG9UiMAQTIQQIgxDsCkFQ%2BQSg1B110NMAwWDTBJxsKAmITdICrFQKkeod9eCoCQbAvW8BVh2F3tkFwQpJh%2BGmKEeY5RKgFAyFkAQiiNFFGyAMNRwxpgyI/gIXcOjjG1FkWY2YBihgJGMbMCxMw%2Bh2MWA46RqctgSDDpwSOpBo6x3jhwY4qgkh%2BgALR%2BkkHqZA3Jx7k3IhAXAhASBYV2FwZYvBW5aCtqQAuRcS7l2KUXSu4ca4BLrsExuzcs7YI7jARAIA7apDdAPCAQ8R6RFYNsMJkTomxPif4RJvBMqpIkXofg1DRDiHoVMxhKh1Dn1YaQMkXxUgIN8RHWu59gkbzdK0gkqBJZ9KiTE4AcTjgJKSR4Xu9BiDpMydk7B%2BdC7FxKSUquHAKmBNEQ3WwtScm5y%2BWYHZQT/lAryUgzIzhJBAA%3D%3D%3D)
```cpp
#include <iostream>
#include <random>
#include <algorithm>
#include <cassert>

int rollTwoDice() {
    static std::random_device rd; static std::mt19937 gen(rd());
    std::uniform_int_distribution<int> d(1,6);
    return d(gen) + d(gen);
}

struct RunningExample {
    enum Next { Start = 0, WaitReroll, WaitQuantity, Done };
    Next next = Start;
    int  result = 0;

    void start() {
        assert(next == Start);
        result = rollTwoDice();
        std::cout << "First roll: " << result << "\n";
        next = (result < 7) ? WaitReroll : WaitQuantity;
    }

    void userRerolls(bool it_does) {
        assert(next == WaitReroll);
        if (it_does) {
            result = rollTwoDice();
            std::cout << "Rerolled: " << result << "\n";
            next = Done;
        } else {
            next = WaitQuantity;
        }
    }

    void userDecidesQuantity(int q) {
        assert(next == WaitQuantity);
        result += std::clamp(q, 0, 5);
        next = Done;
    }

    bool is_done() const { return next == Done; }
};

int main() {
    RunningExample sm;
    sm.start();
    if (sm.next == RunningExample::WaitReroll) sm.userRerolls(false);
    if (sm.next == RunningExample::WaitQuantity) sm.userDecidesQuantity(3);
    if (sm.is_done()) std::cout << "Final result: " << sm.result << "\n";
}
```

* Class rewrites are easy to perform on small programs, hard to perform on larger programs.

---

## Coroutine based interactive implementation.

[godbolt](https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGe1wAyeAyYAHI%2BAEaYxCAAbLGkAA6oCoRODB7evnrJqY4CQSHhLFEx8baY9vkMQgRMxASZPn5cFVXptfUEhWGR0XEJCnUNTdmtQ109xaUDAJS2qF7EyOwc5gDMwcjeWADUJutuTkPEmKwH2CYaAIIbWzuY%2B4fEhuioLBdXt2abDNteewOHkS1TEnxudz%2BDyebjQxEWjhC4NuNwImBYiQMaJh2yYCgUuwAKsiTl4HLsAJIMRJeAj7ADsVhuuxZuyG6BAIFQIPSYMOxPW2F2ADcxF5MAcmddWWyCByUCQEcFMAB9BCvehAi67ADuTEI0UlXy%2BMtJ5OueoNxAZUplMqpNII5liu2CRuZdpZEVQnl2TEtBBVpyY6AAnhBZrs0AwhrsGKhMKoViCbbtTgQlgxXQwAHSi7yYHPqhQq/PiiOShkAERNnpFqDw6D9AZVCi8CkSrgg7M5cKVITVGolh21CEj8cTybpJkZ2ZzAeiTyruwQlZnNY9nsJzf1gdObbYEdT2%2BFS9l8pYqGFmAgACpgnmxZhZpWH2XC/vMAQK%2BsLGmv5mIprvSG7Sqy67umBLJMLSqC7Ny0RMEQ1poCq/q7keE5JpgKYzn%2B6aARau6Goyt4EAgeAKBBv7Vsam71o2bJeIkmLhiekZ4bWnrvmePYgJe14QMKL6/lxdp4FQuwQAuxAcbOMFECuZ4yZWMlnpxIGVggOb7j4N4iX%2BEH0UZtyaaJEI3GadKEniADWNpiVZuyJPCLCUaqBChp2Dn0TKwR0rptDTusy4aJBdZEnZuzAF%2BQYAcQDAqqgETaJgDhHnh/4ZglkUKLZeF8X2tLKoODDoJqhwue87kqp5nYXJyVCuSqVVuUod7kZRL5mYZmm%2BayfFth2rhobQeqhgSwRpGIrbtp2ZWYQm2G4bOBE5RpNY0SZEWDXNI1iONBI0MwtCzcNC3jktU6pmtWYbcBoERcKDZNl4DDqmV9DoCqk44dUGWznxaLEG5zBoj%2BvWPXWz2MbdpZPhA/kipdv0rfhmBtkFZ7Cg9YnUbaA1yr2irFQOH3lcObitTVdXDkKq6MvjYkw02EwNADf4SVJCD7GYsTOrsYBgNpbwhBGkbabph4GbR9Her6ov6VGAixplt2C8LDJuDObgrjmisQ7LUHZnS/6Y9%2BkbRqrq3xVmPMHAAYnr1PtbMOkY14WMgLsYVbX1xsAH42XlHOupJEBjnrWAnKg4YyyZTMWdcSPwrQtCEjqqBVngKwc45dSOMg56ci8ZXvCqWDCjnjzEOglYTIXxf8QQXAAJyt%2Bs9LRYwEC1%2BL4WE/Kb0SSQLAqv5FeUQQxB4BExUCEC/naugECtLEBlierK8xQwHGWLs2%2BMBvEL%2B18wf2cQb0MMEwDYKorCYjeDq0kC8u0J8fP/qntCkJS1Iv4cJegoBYAEcvCGEcJ5OSBMWQpw9ljA4y5v4ZyztXCGYkua93gcFXW9JoFiRlG/XUECzyoXQoQL%2Bnh37mWNn5cOepBDQLNp7YKSCqEoOzrnGWqF1aBSdH7KGLJtqsj4bzKwIVlZoQDLsMBEDCChgHiyHhttmFBUggnG4SMWD6gYHneiz9%2BFuDftqU439FF/0dIvQQ2oZHgMEPI8x59disLTFfG%2Bd8H70Cwd/X%2Bsj7FQPMQQHMbMLbmNMVQ4JzFWLUDEEoY%2Bxs/GQNDJElitBwzrHiXQqSQSDazEjIVBEMIgS8zMA7YIYhVEEG9uYMwRTDjOPdubDKI56k1JMAAVjcAwNpNCNEomuBweYtBODtN4H4DgWhSCoE4NrSw1g2SLGWI8DYPBSBVImYM%2BYtkQDrHWDmXZBzDlHISMMjgkgxmaF4NMjgvAFAgA0Gsy58w4CwCQGgDEdBojkEoO8xInyYi4iMGYLgXAHk0CCtEO5EAIiXNIBEcpxBQycFWfC5giKADyKU0rrNWe8tggh0UMDSbCrAc9gBuDELQO53BeBYG0UYcQGzSD4FOA4PA15qWTMTGlWkqxJn%2BUqLC2gs8XiIo8FgWF088AsGRbwa8xBvRKCrOiQwwBhVGCeXwAwwAFAADU8CYB1Oi%2BasqZCCBEGIdgUgzXyCUGoWFuhWgGA1aYOZlh9CzzuZAeY3JqjUt2AAWnZIg11VhLBmEmVeaIM9o7wHmHYbF6QXBlVGC0UggRlTTH6K0XIaQBCppyCkPNDAph9BiOMSoiaBCdBGJ4ZoegE1surcMbomay0NpbQW8YLbS0lGzfGxZKwJBDJGRcpl1zdiqAAByxADbESQUZnXAF2MCnMXAcwaCkrgQgJBebrC4LMXg6ytB5NINs3Z%2ByjlXt2Sczg5zSDjMjZwW59zHkbOeTARAXJaSOm%2BRAX5/zQisFWNO2d87orICLlwdpOYzC8EwPgZCjY9D8HNaIcQXB6Q2sUCodQTLHWkB1C8RIsqR0cFGQ%2B2F1z0U/tpPBSSoG50LsBcu1d67N0QA8B8%2Bg1oVmHrfSerZOy9nXuvfoO9Y6n03NsK%2B49mzxMcDg5R8dz6BPyflakZwkggA%3D%3D)
```cpp
#include <iostream>
#include <random>
#include <optional>
#include <coroutine>

template <class T>
struct Input {
    std::optional<T> value;
    std::coroutine_handle<> waiter;

    struct Awaiter {
        Input& in;
        bool await_ready() const noexcept { return in.value.has_value(); }
        void await_suspend(std::coroutine_handle<> h) noexcept { in.waiter = h; }
        T await_resume() { T v = std::move(*in.value); in.value.reset(); return v; }
    };
    auto operator co_await() noexcept { return Awaiter{*this}; }

    void supply(T v) {
        value = std::move(v);
        if (waiter) { auto h = waiter; waiter = {}; h.resume(); }
    }
};

struct Task {
    struct promise_type {
        int result = 0;
        Task get_return_object() { return Task{std::coroutine_handle<promise_type>::from_promise(*this)}; }
        std::suspend_always initial_suspend() noexcept { return {}; }
        std::suspend_always final_suspend() noexcept { return {}; }
        void unhandled_exception() { std::terminate(); }
        void return_value(int v) noexcept { result = v; }
    };
    std::coroutine_handle<promise_type> h{};
    void start() { if (h && !h.done()) h.resume(); }
    bool done() const { return !h || h.done(); }
    int  result() const { return h ? h.promise().result : 0; }
    ~Task() { if (h) h.destroy(); }
};

int rollTwoDice() {
    static std::random_device rd; static std::mt19937 gen(rd());
    std::uniform_int_distribution<int> d(1,6);
    return d(gen) + d(gen);
}

Task runningExample(Input<bool>& reroll, Input<int>& quantity) {
    int result = rollTwoDice();
    if (result < 7) {
        bool want = co_await reroll;
        if (want) { result = rollTwoDice(); co_return result; }
    }
    result += co_await quantity;
    co_return result;
}

int main() {
    Input<bool> reroll;
    Input<int>  quantity;
    Task t = runningExample(reroll, quantity);
    t.start();
    reroll.supply(false);
    quantity.supply(3);
    if (t.done()) std::cout << "Final result: " << t.result() << "\n";
}
```

* Compile with `-std=c++20`
* Preserves **structured** code while being **non-blocking** via suspension points.
* Standard coroutine frames are **not trivially copyable/serializable**, cannot be used in every situation.

---

## No calls state machines
[godbolt](https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGe1wAyeAyYAHI%2BAEaYxCAAHGakAA6oCoRODB7evnrJqY4CQSHhLFEx8baY9vkMQgRMxASZPn5cFVXptfUEhWGR0XEJCnUNTdmtQ109xaUDAJS2qF7EyOwc5gDMwcjeWADUJutuTkPEmKwH2CYaAIIbWzuY%2B4fEhuioLBdXt2abDNteewObjEwBIhAQH3Wlxudz%2BDyeblECiUDU%2BMJhPywNBCuyEABVrnjsAB9ACy1zcAAkAJKhbAQULXUnYWa7XYAN1QeHQu0ZzIgXgY6V212IwAUu3q4qeABF9gB2KzymWskyK3YKADuhGQCAgEwImFViq%2BGyxwUe2FCMuJ%2BMJJPJVNp9NZuyxTC8tAIIA1dUNst2VplBwsu1OBCWDBDCrlauDGPW5pxdqJECErrZmazbIMUVo%2Bx%2BG1xPoNjwOcrTs2jSMeQhApvR30TmGxjzpAA08ZXsz3e2y3grQ6CiLtc5UC%2Bsi0Jo3HdpqEHRMBANFWE0nHm4APLW4kdrtb62kXZ4o8AMQzmYHatDeCouwgB5Vu2HqFHTDzE6LeOjlSUz9QI5jvmGxFqeM7KnOC70Muq63GuLYWrsMrYG41JCNS27dn2b4fiBPzFr6TD%2BuW97ptG4aRtWTB/nWDZNuuIpuF2yGoeh262gSRJHsyeKUpuNp8tgR54gAmsoQm7Ke1LYAET4mAArG4Xxspy3K7DxfECUy9KieJknSbJVbqtRKIEPqfqYOW5YsWhGGhBx9pVusoaCsKorSlKCjRp5AB0UkybG6xyv5snRhAqnoLMpwKD4S6eU5oZxnRwQEGGni0HimqoDKeArBAxpWDcbIGrlvroCAIAvAwbwsMSWDsrljzEOg0YlcgZUVSwBBcAAnD16zys%2BjAQM1%2BUJcpHUgK5/DELVKV1XgJx4BEXjVECKUXG6ECtAAbONRVhpgEbEAwW3AIwqqWGdF0hqayp0V8JxeA4uwAEqCkKRjYKorCJPQQikoOE2MD4uIWYOuKtLiCS4usR5CNIgbWjGt0HZ0/qlgGQhcKj1xsq5AgimKErXhNbIRKgniHcQ6W41mKW7F4KIAIoEAAnrjSXOXRbIM4dMVegGGh029H3BMA32/f9pL5UDB1stFsX5SLSWNmyKYOhSNJ0iNmAxWwsFZhraZcAVZOZorgskTTtAZVlOV5ftePZkM5UoIsqVAkCBZmApFjYwpco0MQQxpbbAbmGYCLe5bnuHN7kcKW4UZmL73Py5mj67tgna6wLcduLs8rwzDCNO1mqtwc7bI2WxoRpmY5eZ9uAk512vmnDbtDw3DuKSE75vG0I6yqhnCt656cdyl3mXZY1yvp9XmauxVaCrdHhw%2B37w%2BB9T6WYDyJGRxvhexyfW%2BKSnaeFUve4QEGTdsjzma13Zab9yLWZn9YJErygBgsESBAXyTNoiszZkeDQR55KP15G3e%2B1oB4Z2Ng/c249jpRkXmyIMDkiRki1s6ZWatGJdiEDDN4xJO7pSPD2CmngjxUNtobEh78jxYGQNyTAxIACOXhDCOHZkeFKNDQHEHAbBLmN8vgMxYEwYIstSYHXegwT6EsfqAOlhqSEUiDq3nvAoFgPlMZWSCqLFR4tJYaMwADCqZCzYZz/mvAuCdU54iYAAa0YHvcO7DFrpGPl7TeidL6JywcvQxFDGG0GoGIJQCVsIJJ7BNSuvM7z6kMcYoKJFlGqMsX9axpJbH9zlkvRxHtz6RzcZ406vi9i8P4YQNmbpMAcNSAIAJ8cgmpyTlfT%2BWifK1K4fUwQjSIAj2jEkg6KTdh6PSUY8GJi5Q5Iseo/JNiQAPxKVmMp69AmF0jqeYIYh%2BaTwjqnc%2BBifLf06fs7pITulhMrpXDg8xaCcHkrwPwHAtCkFQJwJSlhrAakWMsMsPweCkG9N8l58x3EgHWOsHyCLkUotRTtfQnBJCfM0LwP5HBeAKBAFAqFWh5hwFgEgNAgDFxkAoBAKliQaX/0MMAMwXAuBQJoF6aIhKIARBxaQCIRziBs04BCoVzARWbgiNoFpUKIVUrYIITcDBaCiuhaQLAK1gDAltoS7gvAsCyKMOIDV%2BBTgODwOyPWArMCqBaatVYPyUqVAFbQZaLwRUeCwAKggxA8AsDFbwa1xAKZKBlJgY1wB3VGBxfMKgBhxQADU8CYE1JuRIjAg0yEECIMQ7ApA5vkEoNQArdCtAMLG0wgLLD6GWoSyA8xUCJGqPq3YABaV25Zq1WEsGYDQHbNxR3bTKLVXhgC4pDf6rADb8ptDlekFw1VRgtFIIEC00x%2BitFyGkAQK6cgpF3QwKYfQYjjEqAugQnQRieGaHoOwl6ajDG6Bu0997n37vGM%2Bk9JQt3zAUCClYEhXnvOxRqvFuxVCxB2u2nakhdjbBZbsNlPkuA%2BQHfffARBiATlNrwElMLSBwoRUi1FZGEXoreRwLFpAvk/LxQSolkK42kHJYgEAHtEirXIJQBlNLQisFWFBmDcHnzIHalweSPkzC8APoQME5VWj8FzaIcQXBi7KeLSodQGry2kE1C8RIQaQMcA%2BbRgVeLNyrS46lVAd5hOwfg4howyG0NoYwx4al9AcMbDw8x6FsxYXwsReR8jGLqNgfo5wRjxK40mZk%2BZ8D0X/OkvmCGtpfhJBAA%3D%3D%3D)

```cpp
#include <iostream>
#include <random>
#include <algorithm>
#include <cassert>

#define STATE_MACHINE(NAME)  void NAME(union Args args = {}) { switch(state) {
#define END_STATE_MACHINE()  default: state = END; return; } }
#define STATE(S)             label ## S: state = (S); case S:


#define NEXT(S)                    do { goto label ## S; } while(0)
#define COND_NEXT(COND, T, F)      do { if (COND) goto label ## T; else goto label ## F; } while(0)

#define DECISION(S)          label ## S: state = (S); return; case S:

#define ACT(DECISION_STATE, METHOD_NAME, TYPE, FIELD) \
  void METHOD_NAME(TYPE FIELD){ assert(state==DECISION_STATE); union Args args; args.FIELD = FIELD; (void)resume(args); }

int rollTwoDice() {
  static std::random_device rd; static std::mt19937 gen(rd());
  std::uniform_int_distribution<int> d(1,6);
  return d(gen) + d(gen);
}


struct RunningExampleSM {
  enum State { S1, S2, S3, S4, END };
  State state = S1;
  union Args {
    bool reroll;
    int userQty;
};

  int  result = 0;
  RunningExampleSM() {
    resume();
  }

  STATE_MACHINE(resume)
    STATE(S1)
      result = rollTwoDice();
      std::cout << "[S1] first roll = " << result << "\n";
    COND_NEXT(result < 7, S2, S4);


    DECISION(S2)
    COND_NEXT(args.reroll, S3, S4);

    STATE(S3)
      result = rollTwoDice();
      std::cout << "[S3] rerolled = " << result << "\n";
    NEXT(END);


    DECISION(S4)
      result += std::clamp(args.userQty, 0, 5);
    NEXT(END);

    STATE(END)
      return;
  END_STATE_MACHINE()

  ACT(S2, do_reroll,       bool, reroll)
  ACT(S4, decide_quantity, int,  userQty)
};

int main() {
  RunningExampleSM sm;

  if (sm.state == RunningExampleSM::S2) {
    std::cout << "Taken reroll decision" << "\n";
    sm.do_reroll(false);
  }
  if (sm.state == RunningExampleSM::S4) {
    std::cout << "Taken decide quantity decision" << "\n";
    sm.decide_quantity(3);
  }
  if (sm.state == RunningExampleSM::END) {
    std::cout << "Final result = " << sm.result << "\n";
  }
}

```

* `DECISION(S)` **yields** and instantly establishes the **resume point** (`case labelS:`).
* `ACT(...)` methods deliver input and **re-enter** the machine.
* `NEXT(...)` and `NEXT(cond, T, F)` specify transitions between states.

---

## 6) `call_return_sm_macros_pure.cpp`

Non-recursive **CALL/RETURN** with return-address stack (actions remain actions)

[godbolt](https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGE6a4AMngMmAByPgBGmMQgAOxcpAAOqAqETgwe3r7%2ByanpAsGhESzRsQm2mPaOAkIETMQEWT5%2BUpXVGXUNBEXhUTHxiQr1jc05bcPdvSVlgwCUtqhexMjsHOYAzCHI3lgA1CYbbk7DxJish9gmGgCCm9u7mAdHxIboqCyX13dmWww7Xn2hzcYmAJEICE%2BGyut3u/0ezzcogUSkaX1hvwegKewIAbpgHCR0XcMRssDRQnshAAVG7U7AAfQAsjc3AAJACSYWwEDCNyZ2Dmez2uNQeHQez5AogXgYGT2N2IwAUewayueABEDnErHENUKTDq9gyGQoWAz8AokkwCMgkHsFAB3Qh2iCTAiYA0676bckhJ7YMIahk0umMlnsrk8oV7clMLy0AggB31D2avaBjWHCx7M4EZYMbParWGrOw0l%2Bymh%2BkQIQx4UNxvCgzRWgHX6bKnJ904jZa2tzIvIp5CEA%2BiuYClPbkADWpA6bi6Xwve2pzYKIexbVXbG07QiLpb2joQdEwEA0g4nU72bgA8kGGbP5/eg6Q9tT3wAxesN1eGnM8CoPYIFffU9g3VAtyYVtd07akiyqJQINQTdtzbTZOy/Q89WPU96AvK8SR%2BMlJ39PYNWwNwOSEDkHwXZdoNgzDfi7FMbV7fs6yLPMCyHJhkNHccSMrJ5WXnSjqNoh8Q1pel3wFak2TvYMpWwd9qQATWUdS9i/DlsECcCTAAVjcb5hVFcU9kU5TVP5HktJ0vSDKMwcjUYzzG1M8zbkbATUQIN1U04w4tUkmi6LCWSw0HDYcy8pcfIshtZXlRV1TVBQiyygA6fTDJLPsXMKotEuFZK/IbCArPQOYzgUHxzyyuKEvK9qG0qm4Kr1YTfTIyk3BuQJAlrOQLBigAlT89km7BqWrQUKrMlK81NepkAAa1ypIvAUBAGUiJgtogOaFrkwUyo6xcuuFSCmJ3FiNipcapoQ%2BLrvK26HowjtWLOxbk2HWb5sBvrr3Is65EmsIIF/Lz/w8z6DhWqqApiIKwDANbJi23LMBYJICAATzh1rkeXb6ujTE083THGNu2o6TvJinlt87rc0wAh1uO7aUiSQ6%2Bbhq62cY76e3TWnudFsX2u%2B%2B6TTNC08CtG07VluWktRu5cJPM9COEkICFzTxaGpR1UA1PBVjhtcUvdG2U3QEAQFeBh3nNLBcRtp5iHQItHeQZ3XZYAguAATgjjY4ggxgIH9snswdggXZANL%2BGIc1jZV048EiLwakLI5jcuWMIESAA2VrVu5gty%2BARgDUsBum%2BT2FevLG5Ti8BxZtlOUjGwVRWCSeghCZe2qsYHwqRCtdb2GwJsEmxJF5GleuAZG4v3pSaGSGkb30zd8hDXoQzFPjZT8kYt2856mnklsL1%2BX1f75TtP8UJYhgUfsuGZ8w/lVNKAgFRKhVABFKwpIioE8FzYgZt76NmNsKPaMQACKJNkF33isJYUqCGoJhNi/DQwDOaTQHiEYAw9R7jyZHbACXNGpsBFh9Us%2BCqQXWZKyTk3IE6YBYZ6aBXCwy1i4AaKqjYiGJnpmbC2VtfZsKsFIhsww05oELoiYE7YzCmQsGfUyWoaDEGGKbWgGFirmDMNoo4zDiG2LcLonyhYzB6LwaosCT5sBzgEY1WROi4in0vlSSQNcu6NgitJWGF9wmc2FF458EA8pnEQRYq%2BN84kiMWrWDYRFFwyJIcVNJ5tLbW1tnExc6jXaaKKeZOx1j9FCD3CZLUqSzaYAlC/axjj7EBKODoxpZlXHuJUfEkG1JoawyyaonJQgwkiOFIU9sVhirVJQAYQmySIG5XQcQLBxN3waHfCZSpTZ1m1N6UMgxkgjF7ApGIFZ3S3G9IuZspI2zlS7NRAco5JyDQDIaW4lxjSPHjKhjDZR4Nxk5MPm/CRiyQ4oCWHUwZwKTIWDhZvO5oZppcgAOKv0CCC4FYLFxwvEe%2BLFq9t67xXgfJeZzpGCIcS/ZZAAqPYoybqqOFBclFVz0WYqXti1pXK9icoeZYksLzgQ6OWXKoFejhmgrGY2JJmYZkwouhATVIjeLEGLmMlKmYYr0h4ZGfhREUriVrCEpc7wGTtPSUuWBnh3zOtoPkhUbh5zzNIFgZA4pMAMgAI5eEMI4Em75jbvj2Hsg51repgu%2BKglgTAQiMO9FVShDBB40JHoTehDooTGqqkBECZpcrPz7C/XN%2BbaFFswBPV2sSp7jP5VoxVTjrHUiYJtRgCCzaxgJKrDIJLRkiKrY6z11AxBKFZilDhES9gVrdCwat88wp1qoUPQtY9m1MlbWE9tjZO2oqVX2gdDAR1Bv2OGyNhBia3rHQICdOC%2BUbsDcGsNEbBBPogHksqS7O7EQIcBddm6OKah3Xm6hjaD0tpAJq09ajU41IFd23RX4QiPIVVY2VgKnFVvw/Unt6K3AjJwcuzmBqb1kJTaBjgCxaCcBMrwPwHAtCkFQJwcylhrAOiWCsHEvweCkCTFx5jCxNogA2BsXK8mlPKZU5XfQnBJAcc0LwXjHBeAKBAMcyTWgFhwFgEgNAhMzxkAoBASzSRrMbMMMAMwXAuDHJoImGIBmICRG06QSIuHiDE04OJwLzBgt3kiNoAkknxOWbYIIO8DBaAhakwGzABdgAggsQZ7gvAsDpqMOIdL%2BAzgODwPiPL3HMCqAJIXNY3HjZVH87QfOrxgseCwP5ggxA8AsFC7wfExBYFKA1ATZzbWjDaYWFQAwyoABqeBMCOjvEkRgg2ZCCBEGIdgbR%2BCCEUCodQ6XdCJAMNN0wAnLD6HzgZyACxUBEwyHlvYABadRYUrtWEsGYDQ727w2LexqLAWWdPDb61ge7cN2ixYyC4D2YxWikCCP6GYAxEgpDSEXJHegscFAYNMfosQhhVDh7UEYTRPAtD0HYcnDAuiNCJ6UDHthKe46GJT5nswJGLGWKsCQLG2NafS7pvYqgAAclc3uV1vjsZzXKuC5SV/93V%2BAiDEF3BI3gxnpOkFk/JxTKnjfybU6xjgmnSCce47p/ThmJMzdIGZxAIAUW7QIOQSg9nrNhFYGsSX0vZcQWQMHLgJlcpmF4J0wg4IXaJAO8IUQ4guBBIT0dtQ/mzukEdK8JIg2hccHY1b/zum7yF3d3sVAwEA8y7lxd4Aivle5VVx4Kz9BNebG1w7qTcwZNyYUybk36mLci5t5wO3RmZsF8j8X0X4/u8mYWMNtIzhJBAA%3D)

```cpp
#include <iostream>
#include <random>
#include <algorithm>
#include <cassert>
#include <vector>

#define STATE_MACHINE(NAME)  void NAME(union Args args = {}) { __sm_dispatch: switch(state) {
#define END_STATE_MACHINE()  default: state = END; return; } }

#define STATE(S)             label ## S: state = (S); case S:

#define NEXT(S)                    do { goto label ## S; } while(0)
#define COND_NEXT(COND, T, F)      do { if (COND) goto label ## T; else goto label ## F; } while(0)

#define DECISION(S)          label ## S: state = (S); return; case S:

#define ACT(DECISION_STATE, METHOD_NAME, TYPE, FIELD) \
  void METHOD_NAME(TYPE FIELD){                        \
    assert(state == DECISION_STATE);                   \
    union Args args; args.FIELD = FIELD;               \
    (void)resume(args);                                \
  }

#define CALL(SUB_START, RETSTATE)  \
  ret_stack.push_back(RETSTATE);                       \
  goto label ## SUB_START;                             \
  label ## RETSTATE: case RETSTATE:


#define RETURN()               do {                    \
  assert(!ret_stack.empty());                          \
  State __ret = ret_stack.back();                      \
  ret_stack.pop_back();                                \
  state = __ret;                                       \
  goto __sm_dispatch;                                  \
} while(0)

int rollTwoDice() {
  static std::random_device rd; static std::mt19937 gen(rd());
  std::uniform_int_distribution<int> d(1,6);
  return d(gen) + d(gen);
}

struct RunningExampleSM {
  enum State { CALLER1, CALLER1_AFTER_CALL, END, S1, S2, S3, S4 };
  State state = CALLER1;

  std::vector<State> ret_stack;

  union Args {
    bool reroll;
    int  userQty;
  };

  int result = 0;

  RunningExampleSM() { resume(); }

  STATE_MACHINE(resume)
    STATE(S1)
      result = rollTwoDice();
      std::cout << "[S1] first roll = " << result << "\n";
    COND_NEXT(result < 7, S2, S4);

    DECISION(S2);
    COND_NEXT(args.reroll, S3, S4);

    STATE(S3)
      result = rollTwoDice();
      std::cout << "[S3] rerolled = " << result << "\n";
    RETURN();

    STATE(S4)
      result += std::clamp(args.userQty, 0, 5);
      std::cout << "[S4] final += " << std::clamp(args.userQty, 0, 5) << "\n";
    RETURN();


    STATE(CALLER1)
      std::cout << "[CALLER1] STARTING CALLL\n";
      CALL(S1, CALLER1_AFTER_CALL);
      result = result * 2;
      std::cout << "[CALLER1] 2 * final = " << result << "\n";
    NEXT(END);

    STATE(END)
    return;

  END_STATE_MACHINE()

  ACT(S2,        do_reroll,       bool, reroll)
  ACT(S4,decide_quantity, int,  userQty)
};

int main() {
  RunningExampleSM sm;

  if (sm.state == RunningExampleSM::S2) {
    std::cout << "Taken reroll decision\n";
    sm.do_reroll(false);
  }

  if (sm.state == RunningExampleSM::S4) {
    std::cout << "Taken decide quantity decision\n";
    sm.decide_quantity(3);
  }

  if (sm.state == RunningExampleSM::END) {
    std::cout << "Final result = " << sm.result << "\n";
  }
  return 0;
}

```

* **CALL** pushes the caller’s **return state** and jumps to callee start.
* **RETURN** pops the return state and continues at the caller.
* Keeps subroutines without recursion and stays **serializable**

---

## Recursive state machine (push down automata)

[godbolt](https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGISQCcpK4AMngMmAByPgBGmMQgABwA7KQADqgKhE4MHt6%2B/kEZWY4CYRHRLHEJKbaY9qUMQgRMxAR5Pn6BdQ05za0E5VGx8UmpCi1tHQXdEwNDldVjAJS2qF7EyOwc5gDM4cjeWADUJrtuThPEmKxn2CYaAIJ7B0eYp%2BfEhuioLHcPzzM%2BwYhy8JzObjEwBIhAQf129yeLxBbw%2BblECiUbX%2BSKBrzB7whbBYJAAnjjAcDQeDzgA3TAOEgUgF7LA0CLHIQAFUeXOwAH0ALKPNwACQAkpFsBBIo9BdhlsdjrTUHh0MdZfKIFyEHgFFzSWlMOYAGzHObIADWpGOXgYOWOj2IwAUx1aLo%2BABFTskrMlPYqTL7zQB3QjIBAQOYETCB30soFs8LvbCRT387m8gXCsWS6WK45spheWgEEDmloxr3HVOes4WY7XAgbBj1n3eoN1pG43ZJjmZvkQIQFpWjsdKgxxWinIF7Tnl6OE3beofLNsY95CEAsnt995SgAaXNX49PZ6VPx9DehRGOk/qM92c6Ebc7xxDuvoEA0a93mHZ7xuAA8mm/KHsewFpjaXI2gAYiOo6XkGDZ4FQxwQJBAbHDeqB3kwU6PnOXJtvUSjYagt73tOexzrBr7%2Bu%2Bn6YN%2Bv7PH%2BAHHJ62BuOKQjiiBJ7nnhBE0UC84VkwVZnCuw5tk2LbrkwZFbjulJ7o6bjHlxPF8SBGY8nyNrylyopAemmrYNBACayiWccsHitgIRYSYACsbgAkqKpqscxmmeZcrSlyNnYPZjnOWuwZCdFY5uR5TxjkpWIEBATb8haloAHQxEwVoQMsAC0dyLl60mcdxvH8ZE%2BlZmuuwNjFZ5xZ5o52g6Toeu6Chtl1mUOU5HbLmFA1to1SrNQlo4QN56DLGlGXZbllr5UVCLXAoPjMQAVAQuoKDaXV1Q1Y0naOE2PON/qqay/7JscbiPCEIRDnIFg1QASjBxzvdgXIDgq43uS1C3zS0VqZWkXgKAg/I5XlEzoCAIAsEwlqYPybUAI5eMa5xCOEwD0Nygp3PlR2A/FF0SeDoNLYteWFcVlZLt6QivR9xH1acQOTSVZU/X9Bn3Fz57nUqIOYAQ6Vg1lcPLYza2YBtbBRjLR1i42ksKSLp0xRrVGEWJAv/eWG7fb9JvXexd0C3I72RPlp1IVFusUy1SXxClYBgBLUsLZgLBpAQpJk6NrtNTzVMLaItD0CzFaI8jqD0qrdO0%2BDcuh/VGu%2B9LdMZGksNLflr6R%2BLMuZensvFwr2DrZtqdWuTGvycQrY6%2BHEeU2%2BH50MxP7XYmt0cg9T3YKFEBbdHYhx6xALhAQjaeLQXIhqgnp4FsjvIcDlabwnSNfAwPwsPyWC0pv7zEOgbbRvvCNIywBBcAEAS7Mk2GMKl6BZ1YvMEInNq/BiCnwXmfPUBBiB4BiF4RoEIF53ELBALgpATTq0mq3BgSDgCMEDJYbBuD6wsiut2R4VwvAOG%2Bnae0RhsCqFYGkImgoryqSVFDAmxwdR6gNEaas71qEEzoQwphRDSFsPtAIR0zpXQ70mkqGIqBPCa2IMvURVMlQLzYViAAisHNRl06zZzERWYgFDF74yMETLkzDZHqOOJo%2BupZqwaH0aOTRhB4iSRyDIoaLijF2JakqRgPhOTMyvPdR6IRsDvRQREseMT%2BSPFgnyd6/JR4hBtLWG0QhYlCDMNk3Y2TJDtlcUqfoVY%2BZDXSdErgaiWr/SFCKCUUpUpK02qxMc/0hxcEDHI0cjjF5lRUbHVe69L4l38aeB%2BKB1iDPOBCGcZg3IWByW5b0NBiATCXrHas5gzBogWQMg55xFlxVbGYJZkzRyYTAtgI8rSNpOIWakTk%2BTOSSHQWxOx2lKoCTyZ8scNzwIQF6tcYZtAClFM%2BYEzkQshy7A6eOI5Qzl6jI3lvAF45ploFgcctwpzXIrKfK5b0YLl6YHVGVPZeLNaPLmR5E5eyzlMquUqW29sJl/y%2BWOH5ukHZCA%2BTCpUyLLBlWxQYQOILpGZShvEXRpIbQaBtK5TFY5sWzJpUywlAq1nHHZGIGcVghrUohAs8VDCpUuhlTo4OirlWBnmYyi5zLnWsvNlyO2DtoXGLKXC6pMTEVqoAUjHF9KFlaosP62pJLYWPE%2BpKAA4nEp6LrLlctPOk7pNoo2JOSdEtJkTVX9LaU8qpkTx6VxLYvLaxw02niFQfGZuLTVOqWYSqNur9k1v1dRY1FyaXIsdfirVbhzlpphcC2s3q7FdKnTCzBdTJq1hqnyRpuYWmIs7K46ZWMcb8iDsQCEFjCaYGJogmOcdqwMBLLQA9rjj1WMFEjcp7xFzb3jH0zBms/YV0zrXRcrit2TQcVW996bi3Njbt%2BvOGca6rTrlWwDJDuWNvpIyQ95wd32mxujO9eMCaPv%2BAiaDGVF1U34QwGhwAhGByYWBoVVcIZQxhpnaZKM0YY2wzjI9BHT3WNJssZufSSO/rg3ceuKsdp7SEwE5DrCNLHgfXxp9IA8k2jPD8fkZLY7qfHAozwNptO0ERSKRTvHibPukFgZAap0bY0MI4W19jBDqdlcQeVc8rr%2BPnoIY4KNwj0cmhRqjNHGGnuYQoeEXKWqoXQpFzKb6HWGO9MFwR9DaPhefeZ6xz6zBxnA%2BXROobNUXK5KjRgyjl6FgZHqHIqbSnmhYJlTTRnqBiCUOTU4k0gModi1GJriXSpDVS7Q9LYWhAqaUxZ1THyWF9PVc2odiyytoywdZ2zxx7OCEIKSarNmsgCHq26%2BL62sD8i245kOCLRotR6zFtC/WEvM23sufmAjRvCMy6p7LKmp1zbsQtsNrbYLhANYOjs/aW34viwMl7DLh3OvcmOpDXYqZfr8dF5DHBVi0E4K5XgfgOBaFIKgTgHlRX4IUOsTYhIgQ8FIGWIn2PViWhALsXYmV2dc%2B5zzk0%2BhOCSAJ5oXgpOOC8AUCAJVjOtCrDgLAJAaBA59zIBQCAiu0jK5QAYIwZguBcCVTQUs8QJcQBiML0gMRQfEFJJwenlvmDW6AjEbQDJGf08V2wQQQEGC0Bt0z0gWAYHAEhLHCX3BeBYBRpY7YxP8DXAcHgekYfieYFUAyWBMfeAL3qOb2g0CvjW48Fgc3kC8AsFt7wekxAFFKE9AHQwhMCbC9WFQAwLoABqeBMAhiAkaQn9P%2BCCBEGIdgUgZCCEUCodQ/vdAoO18Yaw1h9DQIl5AVYqAg7eM4McAqCNpKmApxYMwGgd9AX2QVT0gevDABF1XqBWBV/5R6K7nILhj7TD8Cg0IyZFijBQcUbIAQD/PQAAxoBYEYBIFBOwF/AQfoKYTwToPQaAhPWAyYQYH/CApAtA4AqAtA8AqoP/VYKnDYLYCQHHPHIXf3UXY4VQRIE0AqE0YpQ4BvWtLgTKNgk/CAXAQgEgR8HpXgaXZnUgVndnTnHncQ9nPnXHDgQXUgQnYnUXcXSXBnZvUgOXRAEAWZSGAgcgSgdXZXSIVgbYWg%2Bgxg7CZAZAY4LgVyTKMwXgClHg%2B/PQQfYQGOUfVIFwyfNQc3WfUgEML4NICvcgjgfHOQ83UXICWBbQ44VANCEwhgpg%2BfVg9gzKTgjwJXegYgPg5YAQ5vFnNnDnCQiQ/nGQyghQzgJQqXPIkouwsIqgiolQpnQTUgKvA7LoIAA)

```cpp
#include <iostream>
#include <random>
#include <algorithm>
#include <cassert>
#include <memory>
#include <vector>

#define STATE_MACHINE(NAME)  void NAME(ThisType& stack, union Args args = {}) { switch(state) {
#define END_STATE_MACHINE()  default: state = END; return; } }

#define STATE(S)             label ## S: state = (S); case S:

#define NEXT(S)                    do { goto label ## S; } while(0)
#define COND_NEXT(COND, T, F)      do { if (COND) goto label ## T; else goto label ## F; } while(0)

#define DECISION(S)          label ## S: state = (S); return; case S:

#define ACT(DECISION_STATE, METHOD_NAME, TYPE, FIELD) \
  void METHOD_NAME(TYPE FIELD){                        \
    assert(ret_stack.back()->state == DECISION_STATE);                   \
    union Args args; args.FIELD = FIELD;               \
    (void)ret_stack.back()->resume(*this, args);                                \
  }

#define CALL(SUB_START, RETSTATE)  \
  stack.ret_stack.push_back(std::make_unique<SingleSTM>());  \
  stack.ret_stack.back()->state = SUB_START; \
  state = RETSTATE;         \
  stack.ret_stack.back()->resume(stack);\
  return;                            \
  label ## RETSTATE: case RETSTATE:


#define RETURN()               do {                    \
  assert(!stack.ret_stack.empty());                          \
  stack.callee = std::move(stack.ret_stack.back());\
  stack.ret_stack.pop_back(); \
  stack.ret_stack.back()->resume(stack); \
  return;                            \
} while(0)

#define CALLEE (*stack.callee)

int rollTwoDice() {
  static std::random_device rd; static std::mt19937 gen(rd());
  std::uniform_int_distribution<int> d(1,6);
  return d(gen) + d(gen);
}

struct RunningExampleSM {

  using ThisType = RunningExampleSM;

  union Args {
    bool reroll;
    int  userQty;
  };

  struct SingleSTM {
    int result = 0;
    int iterations = 0;

    enum State { CALLER1, CALLER1_AFTER_CALL, END, S1, S2, S3, S4 };
    State state = CALLER1;

  STATE_MACHINE(resume)
    STATE(S1)
      result = rollTwoDice();
      std::cout << "[S1] first roll = " << result << "\n";
    COND_NEXT(result < 7, S2, S4);

    DECISION(S2);
    COND_NEXT(args.reroll, S3, S4);

    STATE(S3)
      result = rollTwoDice();
      std::cout << "[S3] rerolled = " << result << "\n";
    RETURN();

    DECISION(S4)
      result += std::clamp(args.userQty, 0, 5);
      std::cout << "[S4] final += " << std::clamp(args.userQty, 0, 5) << "\n";
    RETURN();


    STATE(CALLER1)
      std::cout << "[CALLER1] STARTING CALLL\n";
      CALL(S1, CALLER1_AFTER_CALL);
      result = CALLEE.result * 2;
      std::cout << "[CALLER1] 2 * final = " << result << "\n";
    NEXT(END);

    STATE(END)
    return;

  END_STATE_MACHINE()
  };
  std::unique_ptr<SingleSTM> callee = nullptr;
  SingleSTM::State state() {
    return ret_stack.back()->state;
  }
  int result() {
    return ret_stack.back()->result;
  }

  std::vector<std::unique_ptr<SingleSTM>> ret_stack;

  RunningExampleSM() {
     ret_stack.push_back(std::make_unique<SingleSTM>());
     ret_stack.back()->resume(*this);
    }


  ACT(SingleSTM::S2,        do_reroll,       bool, reroll)
  ACT(SingleSTM::S4,decide_quantity, int,  userQty)
};

int main() {
  RunningExampleSM sm;

  if (sm.state() == RunningExampleSM::SingleSTM::S2) {
    std::cout << "Taken reroll decision\n";
    sm.do_reroll(false);
  }

  if (sm.state() == RunningExampleSM::SingleSTM::S4) {
    std::cout << "Taken decide quantity decision\n";
    sm.decide_quantity(3);
  }

  if (sm.state() == RunningExampleSM::SingleSTM::END) {
    std::cout << "Final result = " << sm.result() << "\n";
  }
  return 0;
}

```
* Partial implementation, passing arguments to recursive functions not supprted.
* Has a stack of each active simulated stack frame, but to keep pointers stable it must allocate each stack frame on the heap.
