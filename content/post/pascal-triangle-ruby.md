+++
date = "2013-09-03T19:37:52+08:00"
title = "帕斯卡三角形 (Ruby)"
tags = ["ruby", "alogrithm"]
categories = ["computer"]
+++


# 帕斯卡三角形<a id="sec-1" name="sec-1"></a>

![img](//upload.wikimedia.org/wikipedia/commons/thumb/0/0d/PascalTriangleAnimated2.gif/210px-PascalTriangleAnimated2.gif)

    def pascal_triangle(n, i = 2, result = [[1], [1,1]])
      if n == 1
        [[1]]
      elsif n == 2
        [[1], [1,1]]
      elsif i == n
        result
      else
        current_row = [1]
        (i-1).times do |n|
          current_row << (result[i-1][n] + result[i-1][n+1])
        end
        current_row << 1
    
        pascal_triangle(n, i+1, result << current_row)
      end
    end

-   Image reference: [Pascal-triangle
    Wikipedia-chi](https://zh.wikipedia.org/zh-tw/%25E6%259D%25A8%25E8%25BE%2589%25E4%25B8%2589%25E8%25A7%2592%25E5%25BD%25A2)

<!--more-->

# Output<a id="sec-2" name="sec-2"></a>

    pst = pascal_triangle(7)
    
    puts pst.pretty_inspect
    
    =begin
    [[1],
     [1, 1],
     [1, 2, 1],
     [1, 3, 3, 1],
     [1, 4, 6, 4, 1],
     [1, 5, 10, 10, 5, 1],
     [1, 6, 15, 20, 15, 6, 1]]
    => nil
    =end

# Check<a id="sec-3" name="sec-3"></a>

    pst.map {|row| row.reduce(:+) == 2 ** (row.length - 1) }
    # => [true, true, true, true, true, true, true]

