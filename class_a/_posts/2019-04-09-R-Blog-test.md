
## R 코드를  jupyter로 작성하여 블로그 포스트하기

* 테스트로 진행해봅니다. 


```R
library(tidyverse)
library(nycflights13)
```


```R
(
    flights
    %>% select (year, month, day)
    %>% head(15)
 )

```


<table>
<thead><tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th></tr></thead>
<tbody>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
	<tr><td>2013</td><td>1   </td><td>1   </td></tr>
</tbody>
</table>




```R
(
    mpg
    %>% head(5)
)

```


<table>
<thead><tr><th scope=col>manufacturer</th><th scope=col>model</th><th scope=col>displ</th><th scope=col>year</th><th scope=col>cyl</th><th scope=col>trans</th><th scope=col>drv</th><th scope=col>cty</th><th scope=col>hwy</th><th scope=col>fl</th><th scope=col>class</th></tr></thead>
<tbody>
	<tr><td>audi      </td><td>a4        </td><td>1.8       </td><td>1999      </td><td>4         </td><td>auto(l5)  </td><td>f         </td><td>18        </td><td>29        </td><td>p         </td><td>compact   </td></tr>
	<tr><td>audi      </td><td>a4        </td><td>1.8       </td><td>1999      </td><td>4         </td><td>manual(m5)</td><td>f         </td><td>21        </td><td>29        </td><td>p         </td><td>compact   </td></tr>
	<tr><td>audi      </td><td>a4        </td><td>2.0       </td><td>2008      </td><td>4         </td><td>manual(m6)</td><td>f         </td><td>20        </td><td>31        </td><td>p         </td><td>compact   </td></tr>
	<tr><td>audi      </td><td>a4        </td><td>2.0       </td><td>2008      </td><td>4         </td><td>auto(av)  </td><td>f         </td><td>21        </td><td>30        </td><td>p         </td><td>compact   </td></tr>
	<tr><td>audi      </td><td>a4        </td><td>2.8       </td><td>1999      </td><td>6         </td><td>auto(l5)  </td><td>f         </td><td>16        </td><td>26        </td><td>p         </td><td>compact   </td></tr>
</tbody>
</table>




```R
ggplot(data=mpg) +
geom_point(mapping=aes(x=displ, y=hwy))
```


![png](2019-04-09-R-Blog-test_files/2019-04-09-R-Blog-test_5_0.png)

