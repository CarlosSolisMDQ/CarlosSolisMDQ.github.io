---
layout: post
author: Carlos
---

### Apunte de como usar la librería jfreechart para un linechart común y corriente.

*Primero hay que instalar la librería, si tenés Maven instalado y usas IntelliJ como IDE lo unico que hay que hacer es:
Control+shift+alt+s para abrir "project structure" y de ahí Modules>dependencies>+>library>fromMaven>jfreechart1.0*

{% highlight java %}

import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartPanel;
import org.jfree.chart.JFreeChart;

import org.jfree.chart.plot.CategoryPlot;
import org.jfree.chart.plot.PlotOrientation;

import org.jfree.chart.renderer.category.LineAndShapeRenderer;
import org.jfree.data.category.CategoryDataset;
import org.jfree.data.category.DefaultCategoryDataset;

import javax.swing.*;
import java.awt.*;

public class LineChart extends JFrame{
    public LineChart(){
        super("Ejemplo de linechart con jframe");
        //con esto llamamos el titulo de la ventana

        JPanel chartPanel = createChartPanel();
        add(chartPanel, BorderLayout.CENTER);
        //creamos el panel y le damos la funcionalidad basica, tamano, cierre y posicion

        setSize(800,480);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

    }

{% endhighlight %}

Dentro del JPanel creamos el chart

{% highlight java %}

    private JPanel createChartPanel() {
        String chartTitle = "Cotizacion oficial (ficticia) del dolar en Argentina";
        String categoryAxisLabel = "Dias";
        String valueAxisLabel = "Pesos";
        //los label del chart

        CategoryDataset dataset = createDataset();
        //creamos el dataset

        JFreeChart chart = ChartFactory.createLineChart(chartTitle, categoryAxisLabel, valueAxisLabel, dataset, PlotOrientation.VERTICAL, true, false, false);
        //creamos el chart, solo funciona completando TODOS los parametros del constructor

        //para customizar el chart jfreechart nos permite configurar el objeto plot del chart

        CategoryPlot plot = chart.getCategoryPlot();
        LineAndShapeRenderer renderer = new LineAndShapeRenderer();

        //configuramos el plot del chart seteando el rango de Y, las lineas, colores, fondo y se renderiza
        plot.getRangeAxis().setRange(96, 100);
        plot.setRangeGridlinesVisible(true);
        plot.setRangeGridlinePaint(Color.BLACK);
        plot.setDomainGridlinesVisible(true);
        plot.setDomainGridlinePaint(Color.BLACK);
        plot.setBackgroundPaint(Color.DARK_GRAY);
        plot.setRenderer(renderer);

        return new ChartPanel(chart);
    }

{% endhighlight %}


El dataset es un fragmento de un csv sacado de investing.com que representa el dolar oficial en argentina el dolar oficial es una cotizacion ficticia que informa el gobierno argentino nadie sabe por qué. Lo agrego harcodeado para ahorrarme construir un metodo de ingreso por ahora

{% highlight java %}

    private CategoryDataset createDataset() {
        DefaultCategoryDataset dataset = new DefaultCategoryDataset();
        String series1 = "Dolar oficial";
        //

        dataset.addValue(98.01, series1, "08.09.2021");
        dataset.addValue(97.785, series1, "07.09.2021");
        dataset.addValue(97.94, series1, "06.09.2021");
        dataset.addValue(97.87, series1, "03.09.2021");
        dataset.addValue(97.83, series1, "02.09.2021");
        dataset.addValue(97.596, series1, "01.09.2021");
        dataset.addValue(97.74, series1, "31.08.2021");
        dataset.addValue(97.507, series1, "30.08.2021");
        dataset.addValue(97.364, series1, "27.08.2021");

        return dataset;
    }
{% endhighlight %}

En el main solo levantamos el frame

{% highlight java %}

    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new LineChart().setVisible(true);
            }
        });
    }
}
{% endhighlight %}

La librería **JFreeChart** funciona muy bien. Aún me falta explorarla bastante, pero creo que le voy a dar alguna utilidad para el renderizador de series en archivo que estoy haciendo.