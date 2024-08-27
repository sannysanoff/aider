---
title: Sonnet seems as good as ever
excerpt: Sonnet's score on the aider code editing benchmark has been stable since it launched.
highlight_image: /assets/linting.jpg
draft: true
nav_exclude: true
---
{% if page.date %}
<p class="post-date">{{ page.date | date: "%B %d, %Y" }}</p>
{% endif %}

# Sonnet seems as good as ever

As part of developing aider, I benchmark the top LLMs regularly.
I have not noticed
any degradation in Claude 3.5 Sonnet's performance at code editing.
There has been a lot of speculation that Sonnet has been
dumbed-down, nerfed or otherwise performing worse lately.
Sonnet seems as good as ever, at least when accessed via
the API.

Here's a graph showing the performance of Claude 3.5 Sonnet over time:

<div class="chart-container" style="position: relative; height:400px; width:100%">
    <canvas id="sonnetPerformanceChart"></canvas>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
document.addEventListener('DOMContentLoaded', function() {
    var ctx = document.getElementById('sonnetPerformanceChart').getContext('2d');
    var sonnetData = {{ site.data.sonnet-fine | jsonify }};

    var dates = sonnetData.map(item => item.date);
    var passRate1 = sonnetData.map(item => item.pass_rate_1);
    var passRate2 = sonnetData.map(item => item.pass_rate_2);

    new Chart(ctx, {
        type: 'line',
        data: {
            labels: dates,
            datasets: [{
                label: 'Pass Rate 1',
                data: passRate1,
                borderColor: 'rgb(75, 192, 192)',
                tension: 0.1
            }, {
                label: 'Pass Rate 2',
                data: passRate2,
                borderColor: 'rgb(255, 99, 132)',
                tension: 0.1
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: {
                y: {
                    beginAtZero: true,
                    title: {
                        display: true,
                        text: 'Pass Rate (%)'
                    }
                },
                x: {
                    title: {
                        display: true,
                        text: 'Date'
                    }
                }
            },
            plugins: {
                title: {
                    display: true,
                    text: 'Claude 3.5 Sonnet Performance Over Time'
                }
            }
        }
    });
});
</script>

This graph shows the performance of Claude 3.5 Sonnet on the aider code editing benchmark over time. 'Pass Rate 1' represents the initial success rate, while 'Pass Rate 2' shows the success rate after a second attempt. As you can see, there's no significant decline in performance, suggesting that Sonnet's capabilities have remained stable since its launch.

