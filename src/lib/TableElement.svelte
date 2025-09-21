<script>
    let { top=false, middle=false, bottom=false, self=true, side="left", text="TableElement" } = $props()
</script>

<div
  class={`table-element
    ${top ? ' top' : ''}
    ${middle ? ' middle' : ''}
    ${bottom ? ' end' : ''}
    ${self}
    ${side === 'left' ? 'left' : 'right'}`}
>
  <span class={`${side === 'left' ? 'align-left' : 'align-right'}`}>
    {text}
  </span>
</div>


<style>
    .table-element {
        background: linear-gradient(hsl(0, 0%, 100%), hsl(0, 0%, 98%));
        border: 1px solid;
        height: 2rem;
        border-color: hsl(0, 0%, 75%);
        display: flex;
        flex-direction: column;
        justify-content: center; 
        align-items: center;
        padding-left: 10px;
        padding-right: 10px;
        transition: all 0.2s
    }


    .table-element:hover {
        box-shadow: inset 0px 0px 5px hsl(0, 0%, 75%);
        filter: drop-shadow(0 0 0.05rem hsl(0, 0%, 24%));
    }

    .align-right {
        align-self: end;
        font-weight: 800;
    }

    .align-left {
        align-self: start;
    }

    .right {
        border-top-left-radius: 0px !important;
        border-bottom-left-radius: 0px !important;
    }

    .left {
        border-top-right-radius: 0px !important;
        border-bottom-right-radius: 0px !important;

    }

    .top{
        border-radius: 10px 10px 0px 0px;
        border-bottom: 0px none;
    }

    .self {
        border-radius: 10px;
    }

    .middle {
        border-radius: 0px 0px 0px 0px;
        border-bottom: 0px none;
    }

    .end {
        border-radius: 0px 0px 10px 10px;
    }
</style>