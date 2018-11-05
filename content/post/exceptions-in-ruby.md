+++
title = "exceptions in ruby"
date = "2014-02-16"
slug = "2014/02/16/exceptions-in-ruby"
Categories = []
+++

<p>I inherited some interesting code last week.  A user has the ability to sign into the website with omniauth.</p>


{% codeblock lang:ruby %}
def num
	puts "Enter a number"
	num = gets.chomp.to_i

	if num == 3
		puts "It's a 3!"
		else
			raise "Wrong number, you entered a #{num}"
	end
end

def num2
	num
end

begin
	num2
rescue Exception => ex
	puts ex
end
{% endcodeblock %}

<p>Reference</p>
<a href='http://www.ruby-doc.org/core-2.1.0/Exception.html'>Ruby Exception Class</a>
