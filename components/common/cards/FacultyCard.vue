<template>
    <a :href="`/universities/${item.institution.id}/${item.id}/`" class="f-card">
        <div class="f-card__head">
            <h3 class="f-card__title">{{ item.title }}</h3>
            <i class="ti-heart f-card__heart" />
        </div>
        <p class="f-card__sub-title">MIB School of Management</p>
        <p class="f-card__description">
            The master in insurance & risk management by MIB Trieste School of Management (Italy)
            has been developed with the direct support...
        </p>
        <div class="f-card__footer">
            <span class="f-card__tag">
                <i class="ti-book"></i>
                {{ item.degree.name }}
            </span>
            <span class="f-card__tag">
                <i class="ti-pin2"></i>
                {{ item.institution.address }}
            </span>
            <span class="f-card__tag">
                <i class="ti-time"></i>
                {{ item.duration }} month
            </span>
            <span class="f-card__tag">
                <i class="ti-world"></i>
                On campus
            </span>
        </div>
    </a>
</template>

<script>
export default {
    name: 'FacultyCard',
    props: {
        item: {
            type: Object,
            required: true,
        },
    },
}
</script>

<style lang="scss">
.f-card {
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    border: 1px solid #ececec;
    box-shadow: 0 8px 16px rgb(18 103 142 / 10%);
    display: flex;
    flex-direction: column;
    color: inherit;
    max-width: 900px;

    &:hover {
        color: inherit;
    }

    &__head {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    &__heart {
        font-size: 22px;
    }
    &__title {
        color: var(--main-primary);
    }
    &__sub-title {
        font-weight: bold;
    }
    &__footer {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        column-gap: 10px;

        @media screen and (max-width: 768px) {
            grid-template-columns: repeat(2, 1fr);
            row-gap: 10px;
        }
        @media screen and (max-width: 400px) {
            grid-template-columns: repeat(1, 1fr);
        }
    }
    &__tag {
        display: flex;
        align-items: center;
        font-weight: bold;

        > i {
            margin-right: 10px;
        }
    }
}
</style>
